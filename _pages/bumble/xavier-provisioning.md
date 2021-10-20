---
layout: page
title:  "NVIDIA Jetson Xavier Provisioning"
permalink: "bumble/xavier-provisioning"
order: 3
---

Once you get your NVIDIA Jetson AGX Dev Kit, you will need to setup the SDK Manager on a compatible computer,
and then flash your Dev Kit with the latest L4T (Linux for Tegra) images. Sadly, NVIDIA is often really slow
releasing support for new operating systems, so as of August 2021, you would need an Ubuntu 18.04 image to do the
flashing and use the tools.

Thankfully, they have a docker image that you can use for flashing. 
Instructions based on these: https://docs.nvidia.com/sdk-manager/docker-containers/index.html

1. Download the image from https://developer.nvidia.com/nvidia-sdk-manager-docker-image
   (As of August 2021, we are using SDK Manager version 1.6, and Jetson 4.6)   

2. From a terminal, load the Docker image: 

`docker load -i ./sdkmanager_[version].[build#]_docker.tar.gz `
3. Tag the image as latest, for more convenience

`docker tag sdkmanager:[version].[build#] sdkmanager:latest`
4. Run the sdk manager in CLI mode to confirm that it works, and query the available installation types
`docker run -it --rm sdkmanager --query`
   
5. Connect the provided power cable to your Jetson Xavier board, and connect the USB C port that's next to the
   three power buttons to your computer. Then, boot the Jetson into Recovery mode by pressing and holding the
   middle button, while pressing the outer power button.
   
6. If that checks out, then you want the latest `JETSON_AGX_XAVIER_TARGETS` as follows:
```shell
docker run -it --privileged -v /dev/bus/usb:/dev/bus/usb/ --network host -it --rm sdkmanager --cli install --logintype devzone --staylogin --product Jetson --version 4.6 --targetos Linux --target JETSON_AGX_XAVIER_TARGETS --flash all
```
   
7. This will flash the OS image, and then wait for you to run the `oem-config` process. You can either run this by plugging
in a keyboard and monitor, or by connecting to the exposed serial port: `screen /dev/ttyACM0`
   
8. Once that's done, return to the sdkmanager window, and continue the setup.

9. You should be able to SSH to your device: `ssh robot@192.168.55.1`

10. Once you SSH in, you should do one last `apt-get update && apt-get upgrade`, and then disable a few services
that should not be necessary (like the GUI and docker)
    
```shell
# Disable gnome/GUI login
sudo systemctl set-default multi-user.target

# Disable docker 
sudo systemctl disable docker.service
sudo systemctl disable docker.socket
sudo systemctl disable containerd

# Disable some other random crap you don't need
sudo systemctl disable whoopsie
```    

11. And finally, set up a wifi connection (you'll need an M.2 Wifi module, I recommend an Intel 8265, plus an 
    externally connected antenna.)
    
```shell
sudo nmcli -a d wifi connect [wifi_sssd]
```


NB: If your host computer is Ubuntu, you may experience some frequent connections and disconnections via the USB-Ethernet
interface. To fix that, I recommend disabling the "connect automatically" feature for those Jetson connections within the
provided Network Manager.

---

**How to set up ROS and a Catkin Workspace**

1. Follow the basic instructions to set up ROS Melodic (the only supported version for Ubuntu 18.04) from the official docs:
   1. http://wiki.ros.org/melodic/Installation/Ubuntu
2. Create a catkin workspace with the official instructions
   1. http://wiki.ros.org/catkin/Tutorials/create_a_workspace
3. Be sure to source the workspace from your `~/.bashrc` file.
4. Clone the https://github.com/GoodDogAI/bumble repo into `~/catkin_ws/src`
5. You're going to want to install the Intel Realsense base Linux drivers, using the latest version of the library. (Not just the apt-get install version which can be out of date)
   However, it's okay to use the user-mode UVC library.

   https://github.com/jetsonhacks/installRealSenseSDK/blob/master/installLibrealsense.sh
6. Then, install the Intel Real Sense ROS package from source:
https://github.com/IntelRealSense/realsense-ros#step-2-install-intel-realsense-ros-from-sources

Note, you will need to make a soft link from `opencv4` to `opencv` for the package to compile properly.

```bash
cd /usr/include
sudo ln -s opencv4 opencv
```

7. Run `catkin_make`
8. You should be able to start the robot with `roslaunch mainbot brain.launch`

---


**How to set up the ODrive motor controller**

1. First, connect the battery to the DC power input, plus the AUX pin to the included resistor,
the motors, and then the motor hall effect sensors on the ODrive. The hall effect sensors
from most hoverboard motors are going to have the following connections:

| Wire Color   | Pin|
| ------------ | ----------- | 
| Red         | 5V       |
| Yellow      | A      |
| Blue        | B     |
| Green       | Z     |
| Black       | GND     |

2. The next step is to calibrate the motors, and it's easiest to just temporarily 
connect a USB cable between the Jetson and the ODrive board for this step.
Later, we will set up the CANBUS for reliable communications. 
 
3. Install the ODrivetool as per these instructions:
[https://docs.odriverobotics.com/#downloading-and-installing-tools](https://docs.odriverobotics.com/#downloading-and-installing-tools)
``` 
# I had to adjust the commands as follows to install on the Jetson Xavier
pip3 install Cython
sudo pip3 install --upgrade odrive matplotlib==3.2.2
```
4. Run the instructions below to configure both hoverboard motors. They are adapted from [https://docs.odriverobotics.com/hoverboard](https://docs.odriverobotics.com/hoverboard)

Note, if you run into a PHASE_RESISTANCE_OUT_OF_RANGE error, then you may need to increase the `resistance_calib_max_voltage` value.

```
# Configure Motor 0
odrv0.axis0.motor.config.pole_pairs = 15

odrv0.axis0.motor.config.resistance_calib_max_voltage = 8 # Should be between 4-8 for most hoverboard motors
odrv0.axis0.motor.config.requested_current_range = 25 #Requires config save and reboot
odrv0.axis0.motor.config.current_control_bandwidth = 100
odrv0.axis0.motor.config.torque_constant = 8.27 / 16 # Replace 16 with KV if you know it

odrv0.axis0.encoder.config.mode = ENCODER_MODE_HALL
odrv0.axis0.encoder.config.cpr = 90
odrv0.axis0.encoder.config.calib_scan_distance = 150
odrv0.config.gpio9_mode = GPIO_MODE_DIGITAL
odrv0.config.gpio10_mode = GPIO_MODE_DIGITAL
odrv0.config.gpio11_mode = GPIO_MODE_DIGITAL

odrv0.axis0.encoder.config.bandwidth = 100
odrv0.axis0.controller.config.pos_gain = 1
odrv0.axis0.controller.config.vel_gain = 0.02 * odrv0.axis0.motor.config.torque_constant * odrv0.axis0.encoder.config.cpr
odrv0.axis0.controller.config.vel_integrator_gain = 0.1 * odrv0.axis0.motor.config.torque_constant * odrv0.axis0.encoder.config.cpr
odrv0.axis0.controller.config.vel_limit = 5
odrv0.axis0.controller.config.control_mode = CONTROL_MODE_VELOCITY_CONTROL

odrv0.save_configuration()
odrv0.reboot()

# Now, calibrate the motor, then the hall effect sensors for that motor
odrv0.axis0.requested_state = AXIS_STATE_MOTOR_CALIBRATION
odrv0.axis0.motor.config.pre_calibrated = True

odrv0.axis0.requested_state = AXIS_STATE_ENCODER_HALL_POLARITY_CALIBRATION
odrv0.axis0.requested_state = AXIS_STATE_ENCODER_OFFSET_CALIBRATION
odrv0.axis0.encoder.config.pre_calibrated = True

odrv0.save_configuration()
odrv0.reboot()

# Repeat the configuration for the second motor
odrv0.axis1.motor.config.pole_pairs = 15

odrv0.axis1.motor.config.resistance_calib_max_voltage = 8 # Should be between 4-8 for most hoverboard motors
odrv0.axis1.motor.config.requested_current_range = 25 #Requires config save and reboot
odrv0.axis1.motor.config.current_control_bandwidth = 100
odrv0.axis1.motor.config.torque_constant = 8.27 / 16 # Replace 16 with KV if you know it

odrv0.axis1.encoder.config.mode = ENCODER_MODE_HALL
odrv0.axis1.encoder.config.cpr = 90
odrv0.axis1.encoder.config.calib_scan_distance = 150
odrv0.config.gpio12_mode = GPIO_MODE_DIGITAL
odrv0.config.gpio13_mode = GPIO_MODE_DIGITAL
odrv0.config.gpio14_mode = GPIO_MODE_DIGITAL

odrv0.axis1.encoder.config.bandwidth = 100
odrv0.axis1.controller.config.pos_gain = 1
odrv0.axis1.controller.config.vel_gain = 0.02 * odrv0.axis1.motor.config.torque_constant * odrv0.axis1.encoder.config.cpr
odrv0.axis1.controller.config.vel_integrator_gain = 0.1 * odrv0.axis1.motor.config.torque_constant * odrv0.axis1.encoder.config.cpr
odrv0.axis1.controller.config.vel_limit = 5
odrv0.axis1.controller.config.control_mode = CONTROL_MODE_VELOCITY_CONTROL

odrv0.save_configuration()
odrv0.reboot()

# And repeat the calibration steps for the second motor
odrv0.axis1.requested_state = AXIS_STATE_MOTOR_CALIBRATION
odrv0.axis1.motor.config.pre_calibrated = True

odrv0.axis1.requested_state = AXIS_STATE_ENCODER_HALL_POLARITY_CALIBRATION
odrv0.axis1.requested_state = AXIS_STATE_ENCODER_OFFSET_CALIBRATION
odrv0.axis1.encoder.config.pre_calibrated = True

odrv0.save_configuration()
odrv0.reboot()



```

---

**How to set up an I2S interface microphone with a Jetson Xavier.**

If you purchase a https://www.adafruit.com/product/3421 microphone, then your robot will be able to listen to audio
signals. Note that the "port" (where the sound comes in) to the microphone is on the bottom side of the PCB, so 
you'll want to leave that up and exposed.

I recommend directly soldering some female-female jumper cables (https://www.adafruit.com/product/266) to the microphone 
breakout board, and then plug the connectors in the 40pin expansion header on the Jetson.

![/images/i2smic1.jpg](/images/i2smic1.jpg)

![/images/i2smic2.jpg](/images/i2smic2.jpg)

*Connect according to the pinout below*

| Jetson Xavier      | Mic Breakout |
| ------------------ | ----------- | 
| Pin 17 (3.3V)         | 3V       |
| Pin 20 (GND)          | GND      |
| Pin 12 (I2S2_CLK)     | BCLK     |
| Pin 38 (I2S_SDIN)     | DOUT     |
| Pin 35 (I2S_FS)       | LRCL     |
| Pin 39 (GND)          | SEL      |

Now, on your board, you'll need to enable the pins on the 40 pin connector:
```shell
sudo /opt/nvidia/jetson-io/jetson-io.py
```
Select the 40 pin header, configure for specific hardware, select your microphone, and save the changes.

Next, set your first audio input channel to I2S2, which is the audio connection exposed on the 40-pin header that 
we just enabled.
```shell
amixer -c tegrasndt19xmob sset "ADMAIF1 Mux" "I2S2"

sudo arecord -D hw:tegrasndt19xmob,0 -r 48000 -f S32_LE -c 1 -d 10 cap.wav
```

You should see a signal when you open the recorded `cap.wav` file from your home directory.
![audiotest.png](/images/audiotest.png)

Seems pretty high quality, but a weird click at the start, and some awful DC offset that we can tackle next time.
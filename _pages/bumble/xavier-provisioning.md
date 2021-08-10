---
layout: page
title:  "NVIDIA Jetson Xavier Provisioning"
permalink: "/bumble/xavier-provisioning"
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
`docker run -it --privileged -v /dev/bus/usb:/dev/bus/usb/ --network host -it --rm sdkmanager --cli install --logintype devzone --staylogin --product Jetson --version 4.6 --targetos Linux --target JETSON_AGX_XAVIER_TARGETS --flash all`
   
7. This will flash the OS image, and then wait for you to run the `oem-config` process. You can either run this by plugging
in a keyboard and monitor, or by connecting to the exposed serial port: `screen /dev/ttyACM0`
   
8. Once that's done, return to the sdkmanager window, and continue the setup.

9. You should be able to SSH to your device: `ssh robot@192.168.55.1`


NB: If your host computer is Ubuntu, you may experience some frequent connections and disconnections via the USB-Ethernet
interface. To fix that, I recommend to disable the "connect automatically" for those Jetson connections within the
provided Network Manager.


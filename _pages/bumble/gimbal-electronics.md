---
layout: page
title:  "Brushless Gimbal Pan-Tilt Module"
permalink: "bumble/gimbal-electronics"
order: 3
---

The new gimbal-based pan-tilt module allows you to mount an Intel RealSense camera to the robot,
and have that camera be able to look in two-axes. The gimbal based motors don't have any gearboxes,
which brings some pros and cons.

Pros:
 - Quiet, repeatable operation, with no wear-and-tear
 - Low backlash operation

Cons:
 - Low torque, requiring you to balance the center of gravity
 - More parts and wiring

The cost is actually similar to a servo based pan-tilt head, if you are using nicer Dynamixel servos.

----

**Component List**
 - 2 X [GM3506 Motor w/ AS5048A Encoder](https://shop.iflight-rc.com/ipower-motor-gm3506-brushless-gimbal-motor-w-as5048a-encoder-pro1155?search=3506%20encoder)
 - [BaseCam SimpleBGC 32-bit Tiny Rev. C](https://www.basecamelectronics.com/sbgc32tiny_rev_c/)
 - 2x9 Crimp Connector Housing
 - Female Crimp terminals
 - 2x9 Male Connector Housing


***Encoder Wiring***

 The AS5048A Encoder connects to the SimpleBGC using a SPI interface. That means
 6 connections per board: 3.3V, Ground, MISO, MOSI, CLK, and CS. Each of the two
 encoders will share most of those connections, and only have a separate CS line.

The first thing you'll need to do, is open up the encoder, and replace the 3-pin 
cable with the full 6 pin SPI-cable. Both cables should be included with the motor,
and it's just a matter of opening the case and replacing it.

<figure style="height: 50%">
    <img src="{{ site.baseurl | prepend: site.url }}/images/encoder_plug.png" />
    <figcaption>Plug in the JST-style connector and remount the encoder in the casing</figcaption>
</figure>

Next, you'll have to attach female crimp connectors to all of the pins coming from the encoder.
Double up the 3.3V, Ground, MISO, MOSI, CLK connections from both encoders into one pin each,
and then separate out the CS line from each encoder on it's own pin.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/encoder_full_pinout.jpg" />
    <figcaption>Wiring for encoder module.</figcaption>
</figure>

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/SBGC_Tiny_C_Flat_Top_legend.jpg" />
    <figcaption>Wiring diagram for Simple BGC Tiny Rev C.</figcaption>
</figure>


<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/simplebgc_encoder_wiring.PNG" />
    <figcaption>Pinout map</figcaption>
</figure>

So, what you need to do is map the following pins, reading left to right
 - GND ⇨ GND
 - 5V ⇨ 5V
 - MISO ⇨ RC_SER_RX/RC_ROLL
 - MOSI ⇨ RC_PITCH
 - CLK ⇨ RC_SER_TX/RC_YAW
 - CS (pitch motor) ⇨ AUX2
 - CS (yaw motor) ⇨ FC_ROLL

I used a [9x2 Molex SL female header](https://www.digikey.com/en/products/detail/molex/0022552181/171970) to
attach the encoders to the Simple BGC.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/final_encoder_connector.JPG" />
    <figcaption>The final connector should look like this.</figcaption>
</figure>

---

**Mechanical Setup**

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/camera_parts.png" />
    <figcaption>The final camera system, modelled in Fusion 360 by Taras H.</figcaption>
</figure>

---

**How to configure the camera**

Once you have everything working, you will need to connect a USB cable from your computer, to the SimpleBGC
board, and get the SimpleBGC setup utility working.

1. Start with the Encoders tab
   1. Enable the encoders AS5048A in SPI Mode on the Pitch and Yaw axes
   2. Enable the "skip autodetect" for the encoders
2. Go the Hardware tab
   1. Roll disabled
   2. Pitch and Yaw enabled, inverted, Num Poles = 22
   3. Set the power to ~75
   4. Axis TOP = Y
   5. Axis RIGHT = X
3. Go to the Stabilization tab
   1. Start with the following PID parameters, to be tuned more later
      1. Pitch - P10, I5, D9, Outer P 150
      2. Yaw - P9, I5, D16, Outer P 150
   2. Low pass filter 400 Hz on both Pitch and Yaw
   3. D term LPF at 200Hz on both Pitch and Yaw
4. Go back to the Encoders tab
   1. Calibrate the Efield
   2. Then, center the motors as best as you can, and Calibrate the Offset
   3. Set the Limits to +/- 30 degrees on pitch and yaw, with a 10 degree limit width
5. You want to make sure that you are not seeing any I2C errors, usually they are caused by the IMU Cable getting too close to either a motor, or a motor power connector.
   1. Also check that the Encoders don't have errors, via the Debug/Request State field
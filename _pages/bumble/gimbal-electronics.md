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
 - [GM2804 Motor w/ AS5048A Encoder](https://shop.iflight-rc.com/ipower-gm2804-gimbal-motor-with-as5048a-encoder-pro288?search=2804%20encoder)
 - [GM3506 Motor w/ AS5048A Encoder](https://shop.iflight-rc.com/ipower-motor-gm3506-brushless-gimbal-motor-w-as5048a-encoder-pro1155?search=3506%20encoder)
 - [BaseCam SimpleBGC 32-bit Tiny Rev. C](https://www.basecamelectronics.com/sbgc32tiny_rev_c/)
 - 2x9 Crimp Connector Housing
 - Female Crimp terminals
 - 2x9 Male Connector Housing


***Encoder Wiring***

 The AS5048A Encoder connects to the SimpleBGC using a SPI interface. That means
 6 connections per board: 3.3V, Ground, MISO, MOSI, CLK, and CS. Each of the two
 encoders will share most of those connections, and only have a separate CS line.


<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/SBGC_Tiny_C_Flat_Top_legend.jpg" />
    <figcaption>Wiring diagram for Simple BGC Tiny Rev C.</figcaption>
</figure>



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

The first thing you'll need to do, is open up the encoder, and replace the 3-pin 
cable with the full 6 pin SPI-cable. Both cables should be included with the motor,
and it's just a matter of opening the case and replacing it.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/encoder_plug.png" />
    <figcaption>Plug in the JST-style connector and remount the encoder in the casing</figcaption>
</figure>

Next, you'll have to attach female crimp connectors to all of the pins coming from the encoder.
Double up the 3.3V, Ground, MISO, MOSI, CLK connections from both encoders into one pin each,
and then separate out the CS line from each encoder on it's own pin.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/CatchEB15.jpg" height="300px" />
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



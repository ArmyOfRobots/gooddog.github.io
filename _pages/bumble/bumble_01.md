---
layout: page
title:  "Bumble v0.1"
permalink: "bumble/bumble_01"
order: 5
---

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/dobby0_1.jpg" />
    <figcaption>The first version of Bumble</figcaption>
</figure>

Bumble v0.1 is the first robot design released as part of the gooddog.ai project. It has currently been superceded 
by [Bumble v0.2](https://www.gooddog.ai//bumble/assembly).


Bumble is a three wheeled bot based around NVIDIA's Jetson Xavier Devkit. It features two hoverboard motors for a drive train, plus a small caster wheel for balance. It's meant to be easily assembled from off-the-shelf + 3D printed parts without any special equipment necessary. The total cost is under $2000, which compares quite well to commercial off the shelf solutions like [NVIDIA's Carter robot](https://docs.nvidia.com/isaac/isaac/doc/tutorials/carter_hardware.html) which cost upwards of $10,000.

We chose the Jetson Xavier platform because we want these bots to have the absolute highest amount of GPU and CPU available for a mobile platform, to allow running multiple state of the art networks in real-time. 

Tech Specs:
 - NVIDIA Jetson Xavier (31 TeraOps total compute)
 - ~$1,800 BOM Cost
 - 24V LiFEPO4 battery
 - 2x Hoverboard motors
 - Intel Real Sense D435i
 - Dynamixel Pan-tilt head
 

 [More Information](https://jekyllrb.com/docs/pages/){:target="_blank"}
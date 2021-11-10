---
layout: page
title:  "GoodDog Bumble v0.2 Assembly"
permalink: "bumble/assembly"
order: 3
---

This page will cover the 3D-printing and assembly of the 
GoodDog Bumble v0.2 robot.

---

**Preparing the parts for printing**

You will need to print 1 copy of each of the parts listed on this page:
[GitHub Link](https://github.com/GoodDogAI/bumble-hardware/tree/main/3mf)

That's a total of 9 parts, two of which are the gigantic case top and bottom case pieces.
I have printed everything on an [Ultimaker 2+](https://ultimaker.com/) using
[Yellow Tough PLA](https://www.matterhackers.com/store/l/pro-series-tough-pla-filament/sk/MS59VUVR).

Any printer with a 20x20cm build plate should work just as well, but you should expect around 40 hours of total print time and ~500g of material necessary.

Slicing settings needed:
 - 20% gyroid infill
 - 4 walls
 - Supports are needed on some parts, but it's doable with standard breakaway supports.

*Body Bottom*
<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/body_bottom_supports.PNG" />
    <figcaption>Supports will be needed where the caster wheel attaches, and under the motor mounts, but be sure to use "support blocker" in your slicer to suppress it everywhere else.</figcaption>
</figure>

*Body Top*
<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/body_top_supports.PNG" />
    <figcaption>Supports will be needed on the underside where the antennas and head attaches, and by the microphone mount, but be sure to use "support blocker" in your slicer to suppress it everywhere else.</figcaption>
</figure>

*Body Caster Wheel + Motor Mount*
<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/body_rest.PNG" />
    <figcaption>The rest of the motor mounting and caster wheel mounting parts should be printed as shown, with standard breakaway supports.</figcaption>
</figure>

*Head*
<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/head_supports.PNG" />
    <figcaption>All four of the head components can be printed on one plate. I recommend to print in the orientations shown for the strongest possible prints.
        Only the main "Camera bracket" will need supports, and just go with what your slicer recommends. It's a bit tough to remove, but this is the most complicated part in the assembly.
    </figcaption>
</figure>

---

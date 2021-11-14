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

Any printer with a 20x20cm build plate should work just as well, but you should expect around 60 hours of total print time and ~500g of material necessary.

Slicing settings needed:
 - 20% gyroid infill
 - 4 walls
 - Supports are needed on some parts, but it's doable with standard supports on a single extrusion printer.

Note: If you are using Ultimaker Cura as your slicer, then you can use the same settings we used with the [files here](https://github.com/GoodDogAI/bumble-hardware/tree/main/cura).

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

**Fasteners**

Here are the required fasteners to assemble the robot. I recommend to get a generic M3 and M4 hex cap kit so that you
have a bunch of sizes to choose from and make adjustments and hacks as necessary.


| #  | Type                        | Size     | Q-TY | Comment                                                   |
|----|-----------------------------|----------|------|-----------------------------------------------------------|
| 1  | Button Head Hex Drive Screw | M2.5 x 5 | 2    | Microphone mount                                          |
| 2  | Button Head Hex Drive Screw | M3 x 6   | 2    | BaseCam PCB mount                                         |
| 3  | Button Head Hex Drive Screw | M3 x 8   | 2    | Camera PCB                                                |
| 4  | Button Head Hex Drive Screw | M3 x 10  | 9    | ODrive mount (4), Terminal mount (2), Head connection (3) |
| 5  | Button Head Hex Drive Screw | M3 x 16  |      | Charging plug mount                                       |
| 6  | Button Head Hex Drive Screw | M3 x 25  | 3    | Pololu wheel mount                                        |
| 7  | Button Head Hex Drive Screw | M4 x 8   | 2    | Camera mount                                              |
| 8  |                             |          |      |                                                           |
| 9  | Socket Head Screw           | M2.5 x 5 | 16   | Motors mount                                              |
| 10 | Socket Head Screw           | M4 x 8   | 2    | Power supply mount                                        |
| 11 | Socket Head Screw           | M4 x 16  | 4    | Casae connection                                          |
| 12 | Socket Head Screw           | M4 x 40  | 6    | Wheels clamps                                             |
| 13 | Hex Nut                     | M3       | 4    | Pololu wheel mount (3), Charging plug mount (1)           |
| 14 | Hex Nut                     | M4       | 10   | Wheels clamps (6), Case connection (4)                    |
| 15 | Zip ties short for rires    |          | 16   | Head clip (2), Body clip (14)                             |
| 16 | Zip ties long               | 300mm    | 2    | Battery mount                                             |


---

**Bottom Plate Assembly**

Once you have printed all the parts, you can start assembly.

Install the battery. Use two big zip ties through the integrated clips to keep it tied down.
I used a zip-tie gun set to around 40 pounds of pressure, but just make it firm without deforming the 
battery itself.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/zip_tie_bottom.jpg" />
    <figcaption>You can use a zip tie gun set to 40-50 pounds, or just manually attach the zip ties through the integrated mounts.
    </figcaption>
</figure>

Install the Pololu caster wheel. Take the "Caster wheel base" 3D printed part, and the plastic base of the caster wheel and attach it to the matching hole at the bottom of the plate. Use M3x25 button head hex screws (a full socket cap will probably be too big), and
some matching hex nuts. Once you attach the plastic base, put in the rollers into the caster wheel base, and snap in the retaining clip.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/caster_base_bottom.jpg" />
    <figcaption>
        Use rounded button head M3 screws so that there is no interference with the caster ball.
    </figcaption>
</figure>

Attach the motors to the motor mounts. You'll want the flat part of the
hoverboard motor shaft to go against the bottom of the plate. 
Screw everything in with M4x40 hex cap screws, and M4 hex nuts that go into the traps at the bottom.
(Be sure to clear out all of the support material from the nut traps)

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/bottom_motors_attached.jpg" />
    <figcaption>
        Here I have shortened the wires, and crimped wire "ferrules" to them already.
    </figcaption>
</figure>

Install the [DC-DC converter](https://www.amazon.com/gp/product/B08KZPXK63/ref=ppx_yo_dt_b_asin_title_o06_s00?ie=UTF8&psc=1). 
This component is not strictly necessary, because the Jetson Xavier board runs on 12-20V input, and our battery is around 14V.
However, I've noticed that there can be power spikes at a high enough level to be dangerous to the Jetson Xavier,
so running it through a DC-DC converter is the safest option.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/robot_mounted_psu.jpg" />
    <figcaption>
        If you look in the previous picture, I added some furniture "feet" to keep the PSU more stabilized.
    </figcaption>
</figure>

Prepare your [ODrive 24V](https://odriverobotics.com/shop/odrive-v36) edition by soldering decoupling
capacitors to the motor hall effect sensor terminals. We used 22nf capacitors and followed the [instructions here](https://discourse.odriverobotics.com/t/encoder-error-error-illegal-hall-state/1047/7).
Don't skip this step, if you do, the motor control will appear to work, but randomly after a few minutes of operation,
you will see the `ERROR_ILLEGAL_HALL_STATE` condition.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/odrive_caps.jpg" />
    <figcaption>
        I recommend some inexpensive ceramic capacitor kit from Amazon. Just solder on to the A, B, and Z terminals to ground on
            each motor sensor input.
    </figcaption>
</figure>

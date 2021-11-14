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
        Also, keep the cables going out through the right side, it will be easier to wire later.
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
            each motor sensor input. There is some Kapton tape in the picture to help prevent shorts.
    </figcaption>
</figure>

Mount the ODrive to the mounting posts at the front of the robot. I use M3x10 button head screws, they work
perfectly for this application.

You can use [this USB C to Micro-B cable](https://www.amazon.com/gp/product/B075VRQ6VR/) which has the
perfect length and connectors for this size of robot.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/odrive_mounted.jpg" />
    <figcaption>
       Route the USB cable on the top side of the board, so there is less potential for EMI.
    </figcaption>
</figure>

Build the Terminal Block

The handiest way to attach relatively high current wiring in a safe and easy manner is with
"Anderson PowerPole" brand connectors. You can get this board built and shipped with [jlcpcb.com](https://www.jlcpcb.com) 
for around $15, and it's very handy for future projects.

Instructions:
1. Download the [Gerber Files](https://github.com/GoodDogAI/bumble-hardware/raw/main/terminal_block/5x%20Anderson%20Distribution%20Board%20v39_2021-10-22.zip)
2. Go to [jlcpcb.com](https://www.jlcpcb.com) and order it. You should expect to pay around $2, plus $10 shipping. No special PCB characteristics are required.
3. Assemble the board, you'll need [10x PCB Anderson Connectors](https://www.digikey.com/en/products/detail/anderson-power-products-inc/1335G1/10650394), and [2x connector tabs](https://www.digikey.com/en/products/detail/te-connectivity-amp-connectors/63849-1/271178)
4. You can get [an inexpensive Power Pole crimper](https://powerwerx.com/tricrimp-powerpole-connector-crimping-tool) and a [couple connectors](https://powerwerx.com/anderson-powerpole-connectors-15amp-unassembled) from PowerWerx.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/terminal_block_assembled.jpg" />
    <figcaption>
       Assembled, it should look something like this.
    </figcaption>
</figure>


Attach the Terminal Block

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/terminal_block_mounted.jpg" />
    <figcaption>
       It goes in the front. Put the power input / switch connectors closer to the side as shown to simplify the wiring later.
    </figcaption>
</figure>

Wire your Motors and ODrive

Shorten up the 3 big power wires from your motors as much as you think is prudent, and attach some wire ferrules to the end.
Ferrules are important, because they will effectively turn the multi-strand wire in the motor wires
back to single strand which is very easy to screw into the terminal blocks on the ODrive. It will also help prevent a
single strand of wire getting loose and causing a short-circuit.

I used [this wire ferrule crimper](https://www.amazon.com/gp/product/B073TZ5BBG) which was very cheap on Amazon and 
probably include more crimps than most mortal humans will ever use.

I also added some [ferrite cores](https://www.digikey.com/en/products/detail/w%C3%BCrth-elektronik/74270117/1638926) to
the motor wires, before attaching them to the ODrive board. This helps reduce EMI.

The other 5-stranded wires are used to send the hall effect encoder signal from the motor to the 
ODrive controller. This lets you run the motor efficiently at very low speeds, and also have some
understanding of how many turns of the wheel have been made for odometry. 

My favorite solution here is to use [Molex SL](https://www.molex.com/molex/products/family/sl_connectors)
connectors. They are size-compatible with what are known as "Dupont connectors" 
(those 0.1inch pitch connectors that you use to assemble Arduino circuits, etc). However, they are
more reliable, and you can more easily find [proper crimpers](https://www.digikey.com/en/products/detail/molex/2002187000/14311433).

Check out this [guide on proper crimping](http://www.mattmillman.com/info/crimpconnectors/#sl) and some
additional explanation of crimp connections.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/motor_crimped_connectors.jpg" />
    <figcaption>
       Keep the wires as short as you reasonably can for the least amount of EMI. Long wires basically
act like big antennas, and their signal can couple to other wiring inside of the robot. This is because
a lot of current is getting switched on and off rapidly to drive the motors.
    </figcaption>
</figure>


Build around an 8 inch cable to connect the ODrive (wire ferrules to go into the green block labelled + and -)
and the terminal block which distributes power.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/anderson_to_ferrule.jpg" />
    <figcaption>
       Use some good crimpers to make this a solid cable.
    </figcaption>
</figure>

Quick checkup, at this point you should have the following things done
 - 14V LiFePO4 battery installed
 - Hoverboard motors mounted
 - Caster wheel mounted
 - DC-to-DC Converter installed, wiring not yet created
 - ODrive 24V edition mounted
 - Power distribution board soldered up, and mounted
 - Power connected to the ODrive as shown
 - Each of the motor power leads connected to the ODrive
 - Each of the motor encoders connected to the ODrive
 
--- 

**Finish wiring the bottom case assembly**

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/odrive_connected.jpg" />
    <figcaption>
       Reference of what things should be looking like at this point.
    </figcaption>
</figure>

Next, using 14 or 16 AWG wire, make a cable that will connect the battery to the power distribution board.

I used [these XT60 Pigtails](https://www.amazon.com/gp/product/B07BF8154S) from Amazon, and the crimped
30Amp Anderson PowerPole connectors to the other side as shown.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/xt60_connector_made.jpg" />
    <figcaption>
       These are 14AWG wires, with the Power Pole 30 connectors on the other end.
    </figcaption>
</figure>

Take the Red and Black leads off of the DC-to-DC converter, and crimp on some 30 Amp Anderson PowerPole
connectors to them. 

Plug that into the power distribution board.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/dc-dc-connector.jpg" />
    <figcaption>
       These are 14AWG wires, with the Power Pole 30 connectors on the other end.
    </figcaption>
</figure>

Take the Yellow and Black leads from the DC-to-DC converter, these are going to go into 
the Jetson Xavier AGX board. This board takes a 2.5mm ID, 5.5mm OD Plug, which may be a bit 
bigger than the 2.1x5.5mm plugs which are most common in electronics projects.

The best way I found to accomplish this was using [this cable assembly](https://www.digikey.com/en/products/detail/tensility-international-corp/10-01779/5638255)
from Digi-key, which already has a right-angle connector on it. 

The easiest way to attach these two wires is with some heat shrinking "butt splice" connectors.

I like these official [Molex Perma Seal](https://www.digikey.com/en/products/detail/molex/0191640013/279226) ones, which are also available 
very cheaply from [Waytek Wire](https://www.waytekwire.com/item/30980/Molex-19164-0013-Perma-Seal-Butt-Connector-/) 
with [matching crimpers](https://www.waytekwire.com/item/479/Molex-64016-0041-Perma-Seal-Hand-Crimping-Tool-/). 

You can get some clones of these Perma Seal products on Amazon, for a bit less money. However, I have found that they
are somewhat unreliable. If you do the crimp, and it works (you tug on the wires and they don't come apart), then
you are fine. But maybe 30% of the time, something will go wrong in the crimping process, and you'll have to restrip
the wire and try again. The Molex brand ones, with official crimp tool, work 100% of the time for me.

Be sure to add a ferrite core to the end of the wire where it will attach to the Jetson Dev Kit.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/dc-dc-jetson-connector.jpg" />
    <figcaption>
       Add a ferrite core for better resilience to EMI.
    </figcaption>
</figure>

At this point, you are done with the bottom part of the case! 

---

**Assembling the power switch**

We've gotten ourselves [a nice little rocker power switch](https://www.digikey.com/en/products/detail/e-switch/RSC141D1A81/4029190)
so now it's time to attach it.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/switch_installed.jpg" />
    <figcaption>
       The switch just snaps into the rectangular opening on the top case.
    </figcaption>
</figure>

Build yourself two power leads that will go between the switch and the power distribution board.
You want around 8 inches or so, to give yourself room to open the case later, without being
excessively long to introduce EMI.

Most power switches that you find are going to be using so called "quick connect" 0.25inch spade connectors.
It's a pretty standard part that you'll see on a lot of electronics, and it can handle 30 amps or so pretty reliably, plenty for our application.

I went all out with these [insulated, heat shrinking, spade connectors](https://www.digikey.com/en/products/detail/molex/0191640051/2405835).
You can find cheaper ones, basically any 0.25inch "quick disconnect" spade crimp terminals will work.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/switch_leads.jpg" />
    <figcaption>
       The switch leads should look like this, once you crimp them, and apply a heat gun on the
heat-shrink insulation.
    </figcaption>
</figure>

If that looks good, then you should be able to plug in your battery, the switch leads, and hit the power switch!
You should see a green light on the ODrive board at this point.

<figure>
    <img src="{{ site.baseurl | prepend: site.url }}/images/switch_wired.jpg" />
    <figcaption>
       The switch leads should look like this, once you crimp them, and apply a heat gun on the
heat-shrink insulation.
    </figcaption>
</figure>
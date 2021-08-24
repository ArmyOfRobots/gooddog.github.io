---
layout: post
title:  "Robot following indoors"
date:   2021-08-24 14:03:00 -0700
categories: update
---

Here's a small video of our latest checkpoint. We've previously run into problems where the robot would learn 
some very limited behaviors within one training checkpoint. Ex. you'd train a single checkpoint, and it's behavior
would collapse so it would only drive backwards, or only turn left, or only follow a human within an outdoor
environment (with fewer cluttered objects). This checkpoint (sac-peachy-resonance-379-21504), is the first to have 
a variety of behavior depending on the situation.

<iframe width="560" height="315" src="https://www.youtube.com/embed/Xlq6a826RhU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Project Log:
 - Reduced everything down to 2Hz update rate, so that we don't rattle the pan-tilt module to pieces.
 - Fixed bug with dropout being too high in training. (Now we can set dropout for different parts of the observation space independently.)
 - Discovered some LR schedules and rates which help prevent Q function collapse.
 - Up next: Being able to pass an N-element observation history to the network, so it can start to gain a memory.

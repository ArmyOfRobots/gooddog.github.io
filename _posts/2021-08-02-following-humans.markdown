---
layout: post
title:  "Following humans"
date:   2021-08-02 14:03:00 -0700
categories: update
---

In this video, the robot has learned to keep a human "in-frame" by turning the wheels left and right.
As I move to the left and right, it will slowly turn the motors to keep me centered. This behavior is fully
trained in an end-to-end manner. The camera input goes to a pre-trained vanilla YoloV5s network,
and one of the penultimate layers is then fed into a small MLP network trained with SAC to predict motor speeds and pan-tilt
angles on the head.

One thing we saw was that the training data all came from the backyard, when running the same checkpoint indoors, the robot
basically sits still, or rotates in place without much activity. But, if you take it outside back to where it was trained,
the variety of behaviors increases dramatically.

Another downside, is that the left/right motion does not occur in all orientations or parts of the backyard, it can be location dependent.

Running the sac-amber-snow-284-05632 checkpoint.

<iframe width="560" height="315" src="https://www.youtube.com/embed/kxRaRgLclSM" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Project Log:
 - Fixed bug with calculating the reward function from Yolo intermediate frame.
 - Sped up training with keeping the replay buffer on the GPU.

Next up:
 - Can we train in a "small-offset" simulator?
 - Continue training same checkpoint, potentially with newer bag files
 - Fix bugs with bag recording and message sending reliability

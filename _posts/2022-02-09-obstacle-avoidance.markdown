---
layout: post
title:  "Basic Obstacle Avoidance"
date:   2022-02-09 14:03:00 -0700
categories: update
---

<iframe width="560" height="315" src="https://www.youtube.com/embed/U3l0QFgbJzU" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Here we see our little GoodDog, automatically avoiding an obstacle. 
I'll be honest, this only works fully about 25% of the time, the other 25% of the time it may move towards a direction
which could potentially avoid a collision, and the rest of the time it will just fail to avoid it. 

However, still impressive, as this is purely end-to-end trained on around 6 hours of real-world robot data. The
reward function gives a reward signal when detectable objects (from a YOLOv5 network) are in view, with a bonus
for looking at humans. Additionally, as the human, you are able to press a button on your phone when the robot is
training, to send an additional reward or punishment signal. We often do this when the robot has gotten
stuck on a chair or corner.

(Video from Feb 2nd, using the usual-paper-495 checkpoint)
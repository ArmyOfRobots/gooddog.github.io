---
layout: post
title:  "Exploring the lawn"
date:   2021-07-23 14:03:00 -0700
categories: update
---

Just a shot of the robot exploring the lawn. Running the sac-13200-bs2048-dropout0.88-normalized_env_newbags checkpoint.

<iframe width="560" height="315" src="https://www.youtube.com/embed/hao7AC0BL9k" title="YouTube video player" frameborder="0" allow="accelerometer; autoplay; clipboard-write; encrypted-media; gyroscope; picture-in-picture" allowfullscreen></iframe>

Project Log:
 - Identified and fixed NaNs and large values in the observation/reward buffer
 - Identified throttling issue with bag recording, even with reduced camera framerates
 - Partial success testing the bluetooth reward/penalty button, decided to move to a phone-app based design.

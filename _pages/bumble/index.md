---
layout: page
title:  "What is GoodDog?"
permalink: "bumble/"
order: 0
---


The goal of GoodDog is to build a fully end-to-end trained robot that can be a helper, pet, and companion.
You can think of him something like [Dog from Half Life 2](https://half-life.fandom.com/wiki/Dog).

---

As mentioned in our [project intro](https://www.gooddog.ai//update/project-intro.html]), there has been an explosion
of AI research, but yet very little seems to focus on actually creating a synthetic animal-like consciousness
that acts in the real world. Ex. if you want to make a real AI, it better be capable of moving around in the real
world, and running some RL algorithm end-to-end. Not just generating word tokens or classifying ImageNet. The
closest thing out there so far is probably the [comma.ai body](https://comma.ai/shop/products/comma-body) :)

We have amazing image detecting neural networks acting on
big open datasets, recent advances along the lines of GPT-3, and many more new discoveries. But really someone ought to just
plug all those things together into a single robot entity. This is what this project aims to do.

Simple reinforcement learning algorithms, trained with input from the final hidden
layers of state-of-the-art perception networks, can achieve rich and complex objectives in the 
physical world. We know it will not be easy to design the proper reward functions, to gather the
vast amount of needed training data, or to more deeply explore this promising space.
But this path represents the most promising one yet towards creating synthetic conscious entities with empathy for the common person.

**Progress and Milestones:**
 - [GoodDog Bumble v0.2 - assembled and working](https://github.com/GoodDogAI/bumble-hardware) 
   - 3D printed case, plus off-the-shelf parts, based on a NVIDIA Jetson Xavier dev kit
   - Ultra quiet and reliable design so you can leave it running in your house while you work
 - [ROS based control node](https://github.com/GoodDogAI/bumble)
 - [Soft-actor-critic based end-to-end training](https://github.com/GoodDogAI/rossac)
 - [Android based Bluetooth app to send reward/punishment signals](https://github.com/GoodDogAI/rewardapp)
 - Can follow humans around, with full end-to-end training!

**Next Steps:**
 - Robot to find and get to its charging dock on its own with calibrated rewards
 - Find a better way to pass in more than just the last 5 video frames for longer-range planning and rewards
 - Find a way to incentivize novelty, vs just finding something interesting to stare at
 - Collect 10x more data
 - Make use of audio commands
 - Transformer based language model
   - Connected to the audio command network


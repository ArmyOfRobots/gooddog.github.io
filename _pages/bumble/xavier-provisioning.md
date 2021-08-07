---
layout: page
title:  "NVIDIA Jetson Xavier Provisioning"
permalink: "/bumble/xavier-provisioning"
order: 3
---

Once you get your NVIDIA Jetson AGX Dev Kit, you will need to setup the SDK Manager on a compatible computer,
and then flash your Dev Kit with the latest L4T (Linux for Tegra) images. Sadly, NVIDIA is often really slow
releasing support for new operating systems, so as of August 2021, you would need an Ubuntu 18.04 image to do the
flashing and use the tools.

Thankfully, they have a docker image that you can use for flashing. 
Instructions based on these: https://docs.nvidia.com/sdk-manager/docker-containers/index.html

1. Download the image from https://developer.nvidia.com/nvidia-sdk-manager-docker-image
2. From a terminal, load the Docker image: 

`docker load -i ./sdkmanager_[version].[build#]_docker.tar.gz `
3. Tag the image as latest, for more convenience

`docker tag sdkmanager:[version].[build#] sdkmanager:latest`
4. Run the sdk manager in CLI mode
`docker run -it --rm sdkmanager --ver`

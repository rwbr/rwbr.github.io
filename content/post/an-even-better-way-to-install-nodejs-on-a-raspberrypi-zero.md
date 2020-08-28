---
title: "An even better way to install NodeJS on a RaspberryPi Zero W"
date: 2020-08-28T14:03:06+02:00
draft: true
tags: [nodejs, raspberrypi]
---

Following the guide in my [last post](/post/the-easiest-way-to-install-node-on-a-raaspberrypi) you can safely install NodeJS on a RaspberryPi. If you try this on a RaspberryPi Zero W, this will take a very long time, because it builds NodeJS from source and this device has a very limited CPU performance. Here is a better and faster solution.

<!--more-->

![](/img/bulbs.png)

The RaspberryPi Zero W features an ARM11 CPU, which is fairly slow, compared to the RaspberryPi 3B+ or RaspberryPi 4. This makes the device suitable for application, where the focus is on power consumption. But running CPU intensive tasks on the Pi Zero is not so much fun. 

I recently [described](/post/the-easiest-way-to-install-node-on-a-raaspberrypi) how to set up NodeJS on a RaspebrryPi using [nvm](https://github.com/nvm-sh/nvm). The disadvantage of that method is, that ist takes a huge amount of time when run on a RaspberryPi Zero.

## Here is a better solution

---
title: "An even better way to install NodeJS on a Raspberrry Pi Zero W"
date: 2020-08-28T14:03:06+02:00
tags: [nodejs, raspberrypi]
---

Following the guide in my [last post](/post/the-easiest-way-to-install-node-on-a-raaspberrypi) you can safely install NodeJS on a Raspberrry Pi. If you try this on a Raspberrry Pi Zero W, this will take a very long time, because it builds NodeJS from source and this device has a very limited CPU performance. Here is a better and faster solution.

<!--more-->

![](/img/bulbs.png)

The Raspberrry Pi Zero W features an ARM11 CPU, which is fairly slow, compared to the Raspberrry Pi 3B+ or Raspberrry Pi 4. This makes the device suitable for application, where the focus is on power consumption. But running CPU intensive tasks on the Pi Zero is not so much fun. 

I recently [described](/post/the-easiest-way-to-install-node-on-a-raaspberrypi) how to set up NodeJS on a RaspebrryPi using [nvm](https://github.com/nvm-sh/nvm). The disadvantage of that method is, that ist takes a huge amount of time when run on a Raspberrry Pi Zero.

## Here is a better solution

### Find out, what type of Raspberrry Pi you own

To determine the type of Raspberrry Pi you own, you need an ssh connection to the device. Open the SSH console to run the following command:

```bash
uname -a
```

With this command I can determine the CPU architecture. This way I find out for which architecture NodeJS must be built. Look for a string in the results that starts with **armv**. Example:

```
Linux raspberrypi 5.4.51+ #1333 Mon Aug 10 16:38:02 BST 2020 armv6l GNU/Linux
```

Here I executed this command on a Raspberrry Pi Zero W. The message tells me that this device's CPU arcitecture is **armv61**. In this example I need to download NodeJS built for armv6l. (For Raspberrry Pi 3 or 4 you'll get armv7l as the result).

### Download and install NodeJS

The full archive of all releases of NodeJS can be found [here](https://nodejs.org/dist/). There you can look for the appropriate package for your machine. For the Raspberrry Pi Zero (remember: **armv6l**) the latest release of NodeJS is v11.15.0 (at the time of writing):

![NodeJS for armv61](/img/nodejs11.15.png)

From your host computer establish a remote connection over ssh, then download the archive:

```bash
wget https://nodejs.org/dist/latest-v11.x/node-v11.15.0-linux-armv6l.tar.gz
```

Next extract the files:

```bash
tar -xzf node-v1.15.0-linux-armv6l.tar.gz
```

Copy to **/usr/local**:

```bash
sudo cp -R node-v11.15.0-linux-armv6l/* /usr/local/
```

### Check your installation

To find out if everything went well, check the version of NodeJS:

```bash
node --version
v11.15.0
```

Success! Now clean up your home folder. You don't need these files any longer. 

```bash
rm -rf node-v*
```

Now you have the latest version of NodeJS running on your device.
---
title: "Automatic Wifi hotspot on a Raspberry Pi Zero W to comfortably setup the Wifi settings"
date: 2020-09-02T08:28:33+02:00
---

With the raspberryPi Zero W the configuration of the wifi settings normally works like this: You mount the SD card with your PC. A file called **wpa_supplicant.conf** is created on the boot partition, which contains the necessary parameters. But isn't there a better way? 

 <!--more-->

The normal way to set up a headless Raspberrry Pi Zero W is copying a file call **wpa_supplicant.conf** onto the boot partition of the SD card. 

## The RaspiWiFi project

I found a [project on GitHub](https://github.com/jasbur/RaspiWiFi) called **RasipWiFi**, that makes setting up the WiFi setting right on the device really easy.

From the projects README:

> RaspiWiFi is a program to headlessly configure a Raspberry Pi's WiFi
>connection using using any other WiFi-enabled device (much like the way
> a Chromecast or similar device can be configured).

## My fork of the RaspiWiFI project

I decided to fork that project. My fork of it is available on [my GitHub pages](https://github.com/rwbr/RaspiWiFi). There were no current changes on the original project for the last two years. However the code still works. My fork had to development goals: 

1. Update the web UI to a more modern look
2. Make the project to behave as a captive portal

### 1. Updated web UI

I updated the web UI to use the Bootstrap library, inspired by the work of the GitHub user [swissbyte](https://github.com/swissbyte/RaspiWiFi). I integrated some extra configuration options to set the elements of the footer or the page title with the contents of a configuration file.

### 2. Captive Portal functionality

In my fork of the project I added a simple configuration setting for DNSMASQ, that does the magic. Now, after your client (PC, smart phone, tablet ...) successfully connected to the hotspot, it automatically loads the setup page.

## How to run the project

I will show you here, how you set up the project on your Raspberry Pi Zero W step-by-step.

### Prepare the SD card

Downlad the latest release of Raspberry Pi OS Lite from the [web site](https://www.raspberrypi.org/downloads/raspberry-pi-os/). Next mount the SD card with your PC.

![Mounted SD card](/img/mounted-sd-card.png)

### Burn the image on the SD card

I recommend using a tool called [Balena Etcher](https://www.balena.io/etcher/) to write the image to the SD card. 

![Balena Etcher](/img/balena-etcher.png)

When you start this tool, you first have to select the Raspberry Pi OS image.

![Select the firmware image](/img/firmware-image.png)

**Take care to select the SD card as the target**. Then start the write process. The tool will ask you to enter your account password to start the write operation.

![Flashing the image](/img/etcher-flashing.png)

## Enable SSH on boot

You have to unmount and re-mount the SD card, to proceed with the next step. To automatically enable SSH connections we need to create an empty file called **ssh** on the boot partition of the SD card.

```bash
touch /Volumes/boot/ssh
```

## Initial WiFi setup

This step has to be done just once. Later you will be able to copy the whhole SG card (image) to your devices in order to set them up properly. 

But for the purpose of installation we need an inital WiFi connection to the device, becaus there is no alternative way to install the software.

Create a file on the boot partition of the SD card named ```wpa_supplicant.conf``` like this: (the ```country``` parameter must be set according to your region):

```
country=DE 
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev 
update_config=1 
network={
     ssid="WLAN SSID"
     scan_ssid=1
     psk="WLAN PASSWORD"
     key_mgmt=WPA-PSK
}
```

Replace ```WLAN SSID``` with the SSID of the network you wish to connect to and ```WLAN PASSWORD``` with the appropriate WiFi password.

Unmount the SD card and insert it into the card reader of your Raspberry Pi Zero W. Then connect the device to the power supply to let it boot up. 

## SSH into the device

You need to find out the IP address of the Raspberry pi. Use one of the methods [described in the documention](https://www.raspberrypi.org/documentation/remote-access/ip-address.md). then use this IP address to esablish a SSH connection.

## Configure your Raspberry Pi

Start the configuration tool on your device:

```bash
sudo raspi-config
```

You need to setup:

* user password
* hostname
* optional: time zone
* expand file system

![raspi-config](/img/raspi-config.png)

### User password

Select the menu point to change the user password and set a new password for the user ```pi```.

### Hostname

Select the menu to edit the hostname. Enter a new hostname for your Raspberry Pi. 

![New hostname](/img/new-hostname.png)

### Change time zone

Depending on your location you might wish to set another time zone. Default is Europe/London.

![Time Zone](/img/time-zone.png)

### Finally: Expand file system

This is necessary, because the firmware image, that you wrote on the SD card, is smaller than the absolute size of the card. In my example I use a 16GB card, while the image is just 1.56GB. This step expands the image on the card so that you can use the full size of it.

![Expand file system](/img/expand-filesystem.png)

### Reboot

To finish the setup the Raspberry Pi needs to reboot.

![Reboot the device](/img/finish-reboot.png)

## Install the prerequisites

The next step ist to install all the prerequisites of the RaspiWiFi project. 

```bash
sudo apt update; sudo apt upgrade -y; sudo apt install -y git build-essential
```

Then we are able to clone the project:

```bash
git clone https://github.com/rwbr/RaspiWiFi.git
cd RaspiWiFi
```

## Setup RaspiWiFi

Now you are ready to install the RaspiWifi project on the device.

```bash
sudo python3 initial_setup.py
```

You get guided through the setup. Basically you can press ```ENTER``` on each of the questions. Leaving the options set to their default values is fine. 

When the installer finishes, it ask you to save your changes to the device. Do so (answer "y").

```bash
Are you ready to commit changes to the system? [y/N]: 
```

After som minutes:

```bash
#####################################
##### RaspiWiFi Setup Complete  #####
#####################################


Initial setup is complete. A reboot is required to start in WiFi configuration mode...
Would you like to do that now? [y/N]: 
```

Reboot, then take your smart phone or tablet to scan for WiFi networks nearby. There should be a network named **"RaspiWiFi Setup v1.1"**. 

![Select the RaspiWiFi hotspot](/img/select-hotspot.png)

Select it. If you selected to encrypted the network you need to enter your password. After your client is connected to the RaspiWifi hotspot, a web page automatically pops up.

![Captive portal](/img/capitve-portal-page.png)

(If this page doesn't open automatically, navigate to [](http://10.0.0.1)).

There you can enter the password for the selected network. When you finish the configuration your Raspberry Pi reboots again. After the reboot it is configured to connect to this network. You can login over SSH again. 
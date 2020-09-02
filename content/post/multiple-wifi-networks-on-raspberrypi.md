---
title: "How to configure multiple wifi networks on a Raspberrry Pi Zero W"
date: 2020-08-26T18:36:05+02:00
tags: [raspberrypi]
---

If you install [Raspian](https://www.raspberrypi.org/downloads/raspberry-pi-os/) on a Raspberrry Pi Zero W one essential step is to setup Wifi. You save a configuration file called **wpa_supplicant.conf** on the ```boot```-Partition. But how do you configure multiple networks in one step?

<!--more-->

![](/img/sunset.png)

If you wish to configure multiple Wifi networks, just add another ```network``` section to your **wpa_supplicant.conf** file. Here's an example:

```
country=DE 
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev 
update_config=1 

network={
     ssid="SSID_1"
     scan_ssid=1
     psk="PASSWORD_1"
     key_mgmt=WPA-PSK
     id_str="ID_1"
}

network={
     ssid="SSID_2"
     scan_ssid=1
     psk="PASSWORD_2"
     key_mgmt=WPA-PSK
     id_str="ID_2"
}
```

Of course you will have to set ```SSID_1```, ```SSID_2```, ```PASSWORD_1``` and ```PASSWORD_2``` according to your Wifi router's settings. Use the ```ÌD_1``` and ```ID_2``` properties, to give the networks a good description. For instance "work", "office", "home" or "school" might be sufficient.  

Additionaly you can add a ```priority``` option to the network configuration. This option is helpful, when different Wifi networks are available simultaneously. In this case the network with the highest priority (lowest number) is selected.
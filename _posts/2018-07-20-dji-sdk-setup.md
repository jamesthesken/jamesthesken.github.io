---
layout: post
title: "Painless Walkthrough of DJI's Onboard SDK"
date: 2018-07-20
excerpt: "How to expand the capabilities of your drone with a Raspberry Pi."
tags: [drones, embedded-systems]
comments: true
---

Let's say you have a drone project which includes collecting data from some sensors not provided by DJI. eg. air quality, temperature, humidity, etc. Of course, it would be easy to strap the sensor package on the drone and record blindly. However, there are times when it is useful to have the ability to: transmit the collected data, timestamp/location-stamp the data, or to send commands to the drone based on a sensor's reading. Onboard SDK allows you to do that, however it can be difficult to setup if you are not familiar with Linux or Raspberry Pi's.

### My Setup:
- DJI Matrice 100 (Any DJI Drone really, just need to make sure you have access to a UART port)
- Raspberry Pi Zero w/Raspbian installed (Any model)
- Ubuntu 16.04
- A computer with Windows (only need to enable API access)

### Configuring the Pi:
The pi out of the box won't be able to communicate with the drone over serial. So we configure that, starting with a clean install of Raspbian:

#### Enabling serial access:
From the terminal:
`sudo raspi-config` : go to peripheral access and enable serial communication.
Then 'sudo nano /boot/cmdline.txt'
Here we change the following line from: `dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait`
to: `dwc_otg.lpm_enable=0 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait`

This will make the drone available over /dev/tty/AMA0 
Finally, we set the baud rate to 230400 by adding lines to the end of `/boot/config.txt`:
`sudo nano /boot/config.txt`
add these lines at the bottom: 
`enable_uart=1`
`init_uart_clock=64000000`

<figure>
	<a href="../assets/img/M100.jpg"><img src="../assets/img/M100.jpg"></a>
	<figcaption>DJI M100 UART port schematic.</figcaption>
</figure>

<figure>
	<a href="../assets/img/raspberry.png"><img src="../assets/img/raspberry.png"></a>
	<figcaption>Raspberry Pi GPIO wiring schematic.</figcaption>
	
We'll be using serial communication between the drone and our pi. Therefore, we'll need to use:
- Pin 08 (TX) --> Drone RX pin
- Pin 10 (RX) --> Drone TX pin
- Pin 06 (GND)

This should be the easy part, just be sure that the RX & TX pins aren't switched. 

### Installing OSDK:
In the pi's terminal, download DJI's OSDK Github repo with: 
* `git clone https://github.com/dji-sdk/Onboard-SDK`






#### Enabling DJI API Access:
Register an app for DJI OSDK on <a href="https://developer.dji.com"><b>"DJI's developer site."</b></a> Create a new app in order to get the API keys. After doing so, download DJI Assistant 2 on a Windows machine. Connect the computer to the micro-usb port on the drone. Run the program and navigate to preferences to enable API access. No need for the Windows machine now, unless you want to use the simulation it provides during development.








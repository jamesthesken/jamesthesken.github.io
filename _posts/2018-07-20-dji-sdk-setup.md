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
'sudo raspi-config' : go to peripheral access and enable serial communication.
Then 'sudo nano /boot/cmdline.txt'
Here we change the following line from: 'dwc_otg.lpm_enable=0 console=ttyAMA0,115200 kgdboc=ttyAMA0,115200 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait'
to: 'dwc_otg.lpm_enable=0 console=tty1 root=/dev/mmcblk0p2 rootfstype=ext4 elevator=deadline rootwait'

This will make the drone available over /dev/tty/AMA0 
Finally, we set the baud rate to 230400 by adding lines to the end of '/boot/config.txt':
'sudo nano /boot/config.txt'
add these lines at the bottom: 
'enable_uart=1'
'init_uart_clock=64000000'

### Enabling DJI API Access:
Register an app for DJI OSDK on <a href="https://developer.dji.com"><img src="DJI's developer site."></a> Create a new app in order to get the API keys. After doing so, download DJI Assistant 2 on a Windows machine, 





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

###

Apply the `half` class like so to display two images side by side that share the same caption.

{% highlight html %}
<figure class="half">
    <a href="/images/image-filename-1-large.jpg"><img src="/images/image-filename-1.jpg"></a>
    <a href="/images/image-filename-2-large.jpg"><img src="/images/image-filename-2.jpg"></a>
    <figcaption>Caption describing these two images.</figcaption>
</figure>
{% endhighlight %}

And you'll get something that looks like this:

<figure class="half">
	<a href="http://placehold.it/1200x600.JPG"><img src="http://placehold.it/600x300.jpg"></a>
	<a href="http://placehold.it/1200x600.jpeg"><img src="http://placehold.it/600x300.jpg"></a>
	<figcaption>Two images.</figcaption>
</figure>

#### Three Up

Apply the `third` class like so to display three images side by side that share the same caption.

{% highlight html %}
<figure class="third">
	<img src="/images/image-filename-1.jpg">
	<img src="/images/image-filename-2.jpg">
	<img src="/images/image-filename-3.jpg">
	<figcaption>Caption describing these three images.</figcaption>
</figure>
{% endhighlight %}

And you'll get something that looks like this:

<figure class="third">
	<img src="http://placehold.it/600x300.jpg">
	<img src="http://placehold.it/600x300.jpg">
	<img src="http://placehold.it/600x300.jpg">
	<figcaption>Three images.</figcaption>
</figure>

### Alternative way

Another way to achieve the same result is to include `gallery` Liquid template. In this case you
don't have to write any HTML tags – just copy a small block of code, adjust the parameters (see below)
and fill the block with any number of links to images. You can mix relative and external links.

Here is the block you might want to use:

{% highlight liquid %}
{% raw %}
{% capture images %}
	http://vignette2.wikia.nocookie.net/naruto/images/9/97/Hinata.png
	http://vignette4.wikia.nocookie.net/naruto/images/7/79/Hinata_Part_II.png
	http://vignette1.wikia.nocookie.net/naruto/images/1/15/J%C5%ABho_S%C5%8Dshiken.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}
{% endraw %}
{% endhighlight %}

Parameters:

- `caption`: Sets the caption under the gallery (see `figcaption` HTML tag above);
- `cols`: Sets the number of columns of the gallery.
Available values: [1..3].

It will look something like this:

{% capture images %}
	http://vignette2.wikia.nocookie.net/naruto/images/9/97/Hinata.png
	http://vignette4.wikia.nocookie.net/naruto/images/7/79/Hinata_Part_II.png
	http://vignette1.wikia.nocookie.net/naruto/images/1/15/J%C5%ABho_S%C5%8Dshiken.png
{% endcapture %}
{% include gallery images=images caption="Test images" cols=3 %}

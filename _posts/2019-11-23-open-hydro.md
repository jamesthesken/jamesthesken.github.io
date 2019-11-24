---
layout: post
title: "Low-Cost Hydroponic Monitoring"
date: 2019-11-23
excerpt: "An introduction to building an open-sourced hydroponic monitoring solution."
tags: [hydroponics, embedded-systems]
comments: true
feature: "../assets/post/box-farm.jpg"
---

## My Hydroponic Journey

I spent about a year working day and night on an automated robotic hydroponic garden for my senior design class called Box Farm. After graduating I got to go on a trip to the University of North Dakota to install the Box Farm in a NASA Inflatable Lunar Mars Habitat. I also got to live in the habitat for 4 days with my friends. 

<figure>
	<a href="../assets/post/box-farm.jpg"><img src="../assets/post/box-farm.jpg"></a>
	<figcaption>The Box Farm installed in a NASA habitat.</figcaption>
</figure>

We had quite a bit of press-coverage <a href="https://www.hawaii.edu/news/2019/05/12/space-plants-could-be-astronaut-game-changer/">throughout</a><a href="https://bigislandnow.com/2019/05/12/uh-manoa-develop-space-travel-tool/"> Hawaii</a> which was exciting!

Although I'm no longer working with the team, my interest in hydroponics has yet to cease. One of the most frustrating parts during the design phase of Box Farm was the lack of an expandable hydroponic controller! Blue Lab controllers and others are nice but they tend to be closed source and difficult to integrate for such a custom project.

I want to change that for others. To create an off-the-shelf hydroponic monitoring/control solution that is modular in design, able to adapt for projects like Box Farm.


## $5 Wi-Fi-enabled microcontrollers? Let me see!

After discovering the NodeMCU, I knew my hydroponic controls career would change forever. While this isn't a commercial for them, it's certainly a reason why I think you'll want to stick around for the development of this hydro-controller.

<figure>
	<a href="../assets/post/nodemcu.jpeg"><img src="../assets/post/nodemcu.jpeg"></a>
	<figcaption>A NodeMCU micro-controller.</figcaption>
</figure>

If you're familiar with Arduino controllers, great. It's just like an Arduino Nano with integrated Wi-Fi. If not that's okay too! Follow along and as always, feel free to email me with any questions you have.

We are going to be using this for the development of the first step in our automated hydroponic journey.

## Creating a Web Interface

What's a modern hydroponic controller without a web application? Below is a screenshot of our *first* draft of our user interface:

<figure>
	<a href="../assets/post/web-proto.png"><img src="../assets/post/web-proto.png"></a>
	<figcaption>Prototype web-app</figcaption>
</figure>

We can serve any static web-app we want through the NodeMCU but for now, but for now I'll keep things simple. All I had to do was folllow this quick <a href="https://randomnerdtutorials.com/esp8266-dht11dht22-temperature-and-humidity-web-server-with-arduino-ide/">tutorial</a> and changed it to the Automated Farmer :) . 

Next on my agenda is to:
1. Buy the real sensors needed:
	* pH
	* Electroconductivity
	* Waterproof temperature sensor
	* Air humidity and temperature
2. Integrate Bootstrap CSS to style the web-app.
3. Share the progress along the way.

Want to keep up with where I end up on this journey? I'd love to hear from you! Email me at jamesthesken@gmail.com












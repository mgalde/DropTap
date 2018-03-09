---
layout: page
title: About the Project
tags: [droptap, about, project, class]
date: 2016-03-21
comments: false
---

<center><a href="https://tap.apt-get-sudo.com"><b>DropTap</b></a> is a minimal, network diagnostic tool using a Raspberry Pi and a mobile device.</center>

# DropTap

This project is also visible from https://tap.apt-get-sudo.com
## Executive Summary
Network diagnostics sometimes require technicians to enter confining spaces or otherwise enter areas which will require multiple trips to diagnose network traffic. If a technician needs to verify two machines are communicating, they may need to insert a network tap and then return to the host system to continue diagnostics. This is a waste of time and by deploying the "Drop Tap" the network tech can now accomplish the same task from the palm of his hand by using a mobile device.

Now a network technician can simply deploy this network tap and engage directly limiting the amount of trips necessary to accomplish the task and saving time and money for the project at hand.

## Project Goals
* Build a network tap with a Raspberry Pi 3
* Build a web interface utilizing network traffic as the data population
* Parse data utilizing Node-red project located at https://github.com/node-red/node-red
* Build a mobile application that utilizes the Raspberry Pi tap and the web content hosted within
* Auto generate notifications to alert user to network issues / alert criteria

[Application Requirements](/ApplicationRequirements.md)

[Design Requirements](/DesignRequirements.md)

---
layout: post
title: "CYBR 8480 Project Milestone 1: Design requirements"
date: 2018-03-09
excerpt: "Requirements are extremely important for conducting a successful project. these are the application requirements for the DropTap."
tags: [requirements, design, droptap, project]
feature: https://tap.apt-get-sudo.com/assets/img/Data-Tap-Design-Requirements.png
comments: true
---

# DropTap

This project is also visible from https://tap.apt-get-sudo.com

## High Level Design
![Overall DropTap Overview ](/assets/img/DropTapImages/DropTap1.jpeg)


## Component List
### DropTap
The DropTap is a Raspberry Pi 3 with a USB network dongle which will bridge a connection between a device and its end point

#### Sub-component 1.1 Network cable attached to source device and DropTap
This network cable will provide a medium between the DropTap and the network device

#### Sub-component 1.2 name here
This network cable will provide a medium between the DropTap and the original connection input the previous network device was connected to


## Interface Design Concept
![Overall DropTap UI Concept ](/assets/img/DropTapImages/DropTap2.jpeg)


## Component List
### Component 1 Name here
Packet capture interface

#### Sub-component 1.1 name here
Packet capture interface will show how many packets have been captured so far since the DropTap, the capture will reset after a set amount of packets have been reached (1,000 in this example)

#### Sub-component 1.2 name here
Packet Capture interface will show a progress bar which will live update so that the user can visually see packets pass through the DropTap device

### Component 2 Name here
DropTap basic network tools

#### Sub-component 2.1 name here
Basic network tools will include Tracert command which will then auto populate results into image field above once path is complete. The user can set the desired address which the program would then execute

#### Sub-component 2.2 name here
Basic network tools will include the Ping command which will then auto populate ping results into image field above once path is complete. The user can set the desired address which the program would then execute

### Component 3 Name here
Packet Capture list

#### Sub-component 3.1 name here
The Packet capture list will include a live result of packets based on source IP

#### Sub-component 3.2 name here
The Packet capture list will include a live result of packets based on destination IP

#### Sub-component 3.3 name here
The Packet capture list will include a live result of what basic packets have been recieved

## DropTap Hardware Concept
![Overall DropTap Hardware Concept ](/assets/img/DropTapImages/DropTap3.jpeg)


## Component List
### Component 1 Name here
DropTap component list includes a Raspberry Pi 3

#### Sub-component 1.1 name here
The Raspberry Pi 3 needs a network cable to conduct a network bridge

### Component 2 Name here
USB to Ethernet adapter is connected to the Raspberry Pi

#### Sub-component 2.1 name here
The USB to Ethernet adapter needs a network cable to conduct a network bridge

### Component 3 Name here
Mobile device connection to the Raspberry Pi 3

#### Sub-component 3.1 name here
The mobile device will connect to the Raspberry Pi with a Wifi or Bluetooth connection

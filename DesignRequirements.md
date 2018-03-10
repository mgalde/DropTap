# DropTap

This project is also visible from https://tap.apt-get-sudo.com

## High Level Design
![Overall DropTap Overview ](/assets/img/DropTapImages/DropTap1.jpeg)


## Component List
### DropTap
The DropTap is a Raspberry Pi 3 with a USB network dongle which will bridge a connection between a device and its end point

#### Sub-component 1.1 Network cable attached to DropTap and source
This network cable will provide a medium between the DropTap and the network device

#### Sub-component 1.2 Network cable attached to DropTap and original input
This network cable will provide a medium between the DropTap and the original connection input the previous network device was connected to


## Interface Design Concept
![Overall DropTap UI Concept ](/assets/img/DropTapImages/DropTap2.jpeg)


## Component List
### Component 2 Packet capture
Packet capture interface

#### Sub-component 2.1 Packet Capture Text
Packet capture interface will show how many packets have been captured so far since the DropTap, the capture will reset after a set amount of packets have been reached (1,000 in this example)

#### Sub-component 2.2 Packet Capture bar
Packet Capture interface will show a progress bar which will live update so that the user can visually see packets pass through the DropTap device

### Component 3 network tools
DropTap basic network tools

#### Sub-component 3.1 Tracert tool
Basic network tools will include Tracert command which will then auto populate results into image field above once path is complete. The user can set the desired address which the program would then execute

#### Sub-component 3.2 Ping tool
Basic network tools will include the Ping command which will then auto populate ping results into image field above once path is complete. The user can set the desired address which the program would then execute

### Component 4 Packet Capture list
Packet Capture list

#### Sub-component 4.1 Packet capture Source
The Packet capture list will include a live result of packets based on source IP

#### Sub-component 4.2 Packet capture Destination
The Packet capture list will include a live result of packets based on destination IP

#### Sub-component 4.3 Packet capture Received
The Packet capture list will include a live result of what basic packets have been received

## DropTap Hardware Concept
![Overall DropTap Hardware Concept ](/assets/img/DropTapImages/DropTap3.jpeg)


## Component List
### Component 5 Raspberry Pi 3
DropTap component list includes a Raspberry Pi 3

#### Sub-component 5.1 Raspberry Pi 3 Cables
The Raspberry Pi 3 needs a network cable to conduct a network bridge

### Component 6 Ethernet adapter
USB to Ethernet adapter is connected to the Raspberry Pi

#### Sub-component 6.1 Ethernet adapter Cables
The USB to Ethernet adapter needs a network cable to conduct a network bridge

### Component 7 Mobile device
Mobile device connection to the Raspberry Pi 3

#### Sub-component 7.1 Mobile connection technique
The mobile device will connect to the Raspberry Pi with a Wifi or Bluetooth connection

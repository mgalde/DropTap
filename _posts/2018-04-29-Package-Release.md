---
layout: post
title: "CYBR 8480 Project Milestone 3: Package and Release"
date: 2018-04-29
excerpt: "This project milestone tasks you with polishing your overall application and packaging your product for release."
tags: [Environment, security, droptap, project]
feature: https://tap.apt-get-sudo.com/assets/img/package.jpg
comments: true
---

# Hardware / Software requirements for DropTap

## Hardware

The DropTap makes use of a Raspberry Pi 3 witch it self requires a 32 GB microSDHC UHS-I card to contain the file system. This needs to be a class 10 device as speed will be a issue as the DropTap polls and displays information to a mobile user. The card used for the DropTap can be found [HERE ](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073JWXGNT) which at this time is listed at $12.99.


The Raspberry Pi also needs a power adapter which is included in many Raspberry Pi kits so that the device can function. The kit used for the Raspberry Pi DropTap kit can be found [HERE ](https://www.amazon.com/CanaKit-Raspberry-Power-Supply-Listed/dp/B07BC6WH7V) which at this time is listed at $49.99.


The DropTap makes use of a USB Gigabit Ethernet Adapter . This is needed to create a network bridge that the DropTap connects to so that network communication can continue without delaying current connections. The USB Ethernet adapter for the DropTap can be found [HERE ](https://www.amazon.com/AmazonBasics-1000-Gigabit-Ethernet-Adapter/dp/B00M77HMU0) which at this time is listed at $13.99.


Finally the DropTap needs to use a Ethernet cable to complete the connection and create the bridge . This is used to allow communication to continue to flow from the host system to the host network. The  Ethernet cable used for the DropTap can be found [HERE ](https://www.amazon.com/Mediabridge-Ethernet-Cable-Feet-31-399-15B/dp/B00BI06G1S) which at this time is listed at $5.49. It is important to note that size is not much of a issue as the DropTap should be attached at the local box.


## DropTap Bill of Materials (BOM)

| Component name | Link to Component | Price |
|----------------|---------------------------|-------------------|
| Raspberry Pi Kit | [HERE ](https://www.amazon.com/CanaKit-Raspberry-Power-Supply-Listed/dp/B07BC6WH7V) | $49.99 |
| microSDHC Card | [HERE ](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073JWXGNT) | $12.99 |
| Ethernet Adapter | [HERE ](https://www.amazon.com/AmazonBasics-1000-Gigabit-Ethernet-Adapter/dp/B00M77HMU0) | $13.99 |
| Ethernet Cable | [HERE ](https://www.amazon.com/Mediabridge-Ethernet-Cable-Feet-31-399-15B/dp/B00BI06G1S) | $5.49 |

## Software

The DropTap system is running Raspbian Stretch with the Desktop Option. The kernel version is 4.14 and the current image can be found [HERE. ](https://downloads.raspberrypi.org/raspbian_latest)
The Node Red components are built into the Raspbian operating system which allows any device to run the DropTap feature.

The DropTap also makes use of a mobile application titled DropTap which pulls the relevant information when connected to the DropTap network. The application can be found [HERE. ](https://github.com/mgalde/DropTap/releases/download/v0.5/app-debug.apk)



# Drop Tap Installation

It is important to note that the DropTap platform has been tested and developed to work with the materials found within [the Hardware Requirements](/hardware/software_requirements.md), any additional materials that deviate from this list may need additional steps.

## Establishing a base system

First step is to write the [Raspbian image ](https://downloads.raspberrypi.org/raspbian_latest) onto your [SD card ](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073JWXGNT)and place it within your Raspberry Pi. This is accomplished by using a program like [Etcher ](https://etcher.io/)which is what was used to create the image for DropTap.

Once you boot into the Raspberry Pi you need to connect your [Ethernet Adapter ](https://www.amazon.com/AmazonBasics-1000-Gigabit-Ethernet-Adapter/dp/B00M77HMU0)which will be assigned eth1. This will be needed to establish the bridge.

### We will establish this bridge using the following command

 ```bash
brctl addbr br0
 ```

### Now we want to add eth0 to the bridge so we type to following command

```bash
brctl addif br0 eth0
```

### Now to add the USB network port to the bridge we conduct the following plug

```bash
brctl addif br0 eth1
```

### Now we need to prep the network connections, lets start with the eth0 and place it in promiscuous mode

```bash
ifconfig eth0 0.0.0.0 up promisc
```

### Ok and now lets do eth1 and place it in promiscuous node_modules

```bash
ifconfig eth1 0.0.0.0 up promisc
```

### Now lets put our Raspberry Pi as a man in the middle within the bridge

```bash
echo 8 > /sys/class/net/br0/bridge/group_fwd_mask
```

## Setting up Node-Red

[Node-Red ](https://nodered.org/)is a flow-based programming tool, original developed by IBM’s Emerging Technology Services team and now a part of the JS Foundation. Flow-based programming is a way of describing an application’s behavior as a network of black-boxes, or “nodes” as they are called in Node-RED. Each node has a well-defined purpose; it is given some data, it does something with that data and then it passes that data on. The network is responsible for the flow of data between the nodes.

Run node red from the shell using the command

```bash
node-red Start
```

This will run a server which can be found on the local host as localhost:1880

Next we need to install Node-Red palettes which will allow the use of a user Interface, select Manage Palette from the menu in the upper right as shown below:

![Manage Menu  ](/assets/img/DropTapImages/Product/DropTap2.png)

Select install and search for Node-Red-Dashboard, then select install to the result that matches the following:

![Select Menu  ](/assets/img/DropTapImages/Product/DropTap3.png)

You can import the DropTap code by copying the following text and entering it under the import function

```XML
[{"id":"6fce2b6c.bf27d4","type":"ui_chart","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":1,"width":0,"height":0,"label":"Drop-Tap","chartType":"line","legend":"false","xformat":"auto","interpolate":"linear","nodata":"","dot":false,"ymin":"","ymax":"","removeOlder":"2","removeOlderPoints":"","removeOlderUnit":"60","cutout":0,"useOneColor":false,"colors":["#1f77b4","#aec7e8","#ff7f0e","#2ca02c","#98df8a","#d62728","#ff9896","#9467bd","#c5b0d5"],"useOldStyle":false,"x":680,"y":60,"wires":[[],[]]},{"id":"78ef122a.5d202c","type":"ui_gauge","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":2,"width":"6","height":"4","gtype":"gage","title":"Internal","label":"p/sec","format":"{{value}}","min":0,"max":"50","colors":["#00b500","#e6e600","#ca3838"],"seg1":"30","seg2":"40","x":692,"y":125,"wires":[]},{"id":"6eead369.66c4fc","type":"ui_gauge","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":3,"width":"6","height":"4","gtype":"gage","title":"External","label":"p/sec","format":"{{value}}","min":0,"max":"50","colors":["#00b500","#e6e600","#ca3838"],"seg1":"30","seg2":"40","x":691,"y":186,"wires":[]},{"id":"20f6f7c3.5bd7f8","type":"inject","z":"553a6fa6.62e6d","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"x":230,"y":640,"wires":[["fdb97867.9c6dc8"]]},{"id":"fdb97867.9c6dc8","type":"exec","z":"553a6fa6.62e6d","command":"cat /etc/dhcpcd.conf","addpay":false,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":456,"y":639,"wires":[["a5d35868.c0f168"],[],[]]},{"id":"a5d35868.c0f168","type":"function","z":"553a6fa6.62e6d","name":"","func":"var lines = msg.payload.split(\"\\n\");\nvar data = [];\n\nfor(var i=0; i< lines.length; i++){\n    if(lines[i].indexOf(\"interface eth0\") != -1)\n        break;\n}\n\nif(i != lines.length){\n   for(i; i< lines.length; i++){\n        var tmp = lines[i].split(\"=\");\n        if(tmp.length==2){\n            var value = {};\n            value.text = tmp[0].trim();\n            value.payload = tmp[1].trim();\n            data.push(value);\n        }\n    } \n}\n\nif(data.length != 3)\n msg = null;\nelse\n msg = data;\n\n\n \nreturn msg;","outputs":"3","noerr":0,"x":650,"y":620,"wires":[["1495d323.c396dd"],["1495d323.c396dd"],["1495d323.c396dd","b4440167.5940e"]]},{"id":"1495d323.c396dd","type":"switch","z":"553a6fa6.62e6d","name":"","property":"text","propertyType":"msg","rules":[{"t":"eq","v":"static ip_address","vt":"str"},{"t":"eq","v":"static routers","vt":"str"},{"t":"eq","v":"static domain_name_servers","vt":"str"}],"checkall":"false","outputs":3,"x":829,"y":618,"wires":[["44b160be.5e5f4"],["1984f2cb.81f37d"],["1d93369d.ad03b9"]]},{"id":"b088bf7f.747ab","type":"ui_text_input","z":"553a6fa6.62e6d","name":"ip_address","label":"IP Address","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1053,"y":494,"wires":[["fd94e70.a4a0d18"]]},{"id":"a4d0b7e3.254958","type":"ui_text_input","z":"553a6fa6.62e6d","name":"router","label":"Router","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1093,"y":614,"wires":[["29596487.70e88c"]]},{"id":"29bbaa89.588376","type":"ui_text_input","z":"553a6fa6.62e6d","name":"dns","label":"DNS","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1053,"y":754,"wires":[["cd04d770.9b8b78"]]},{"id":"4a92297a.40a768","type":"exec","z":"553a6fa6.62e6d","command":"sudo sed -i ","addpay":true,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":1293,"y":614,"wires":[[],[],[]]},{"id":"44b160be.5e5f4","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"ip_address\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":873,"y":494,"wires":[["b088bf7f.747ab"]]},{"id":"1984f2cb.81f37d","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"router\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":973,"y":614,"wires":[["a4d0b7e3.254958"]]},{"id":"1d93369d.ad03b9","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"dns\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":953,"y":674,"wires":[["29bbaa89.588376"]]},{"id":"fd94e70.a4a0d18","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static ip_address={{flow.ip_address}}/static ip_address={{payload}}/g;' /etc/dhcpcd.conf","x":1233,"y":494,"wires":[["4a92297a.40a768"]]},{"id":"29596487.70e88c","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static routers={{flow.router}}/static routers={{payload}}/g;' /etc/dhcpcd.conf","x":1133,"y":554,"wires":[["4a92297a.40a768"]]},{"id":"cd04d770.9b8b78","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static domain_name_servers={{flow.dns}}/static domain_name_servers={{payload}}/g;' /etc/dhcpcd.conf","x":1153,"y":674,"wires":[["4a92297a.40a768"]]},{"id":"63a7f97e.0afe28","type":"link in","z":"553a6fa6.62e6d","name":"","links":[],"x":281.5,"y":582,"wires":[["fdb97867.9c6dc8"]]},{"id":"c87a8a93.7cac08","type":"ui_button","z":"553a6fa6.62e6d","name":"reboot","group":"2b4d2ef5.e89192","order":0,"width":"3","height":"1","passthru":false,"label":"Reboot","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":276.6666564941406,"y":788.5555686950684,"wires":[["230d077b.ee6328"]]},{"id":"230d077b.ee6328","type":"exec","z":"553a6fa6.62e6d","command":"sudo reboot","addpay":false,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":487.22217178344727,"y":788.8888463973999,"wires":[[],[],[]]},{"id":"648b2feb.35d34","type":"ui_button","z":"553a6fa6.62e6d","name":"refresh","group":"2b4d2ef5.e89192","order":0,"width":"3","height":"1","passthru":false,"label":"Refresh","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":91.44442749023438,"y":707.332911491394,"wires":[["39749098.adc83"]]},{"id":"4998eff1.1e7f1","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"3","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"","name":"","x":995.7777442932129,"y":792.5553007125854,"wires":[]},{"id":"b4440167.5940e","type":"change","z":"553a6fa6.62e6d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":858.5554542541504,"y":711.4442138671875,"wires":[["4998eff1.1e7f1"]]},{"id":"39749098.adc83","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"300","timeoutUnits":"milliseconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":258.8888740539551,"y":707.4445114135742,"wires":[["fdb97867.9c6dc8"]]},{"id":"16267357.89b96d","type":"exec","z":"553a6fa6.62e6d","command":"sudo tcpdump -n -i eth1 ip and not net 1.1.1.1 and not net 8.8.8.8 and not net 192.168.3.1 and not net 192.168.3.25","addpay":false,"append":"","useSpawn":"true","timer":"30","oldrc":false,"name":"TCPDUMP","x":360,"y":360,"wires":[["7a6903c9.162bac"],[],[]]},{"id":"2eff459a.0c6a8a","type":"ui_button","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":0,"width":0,"height":0,"passthru":false,"label":"Traffic Dump","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":120,"y":380,"wires":[["16267357.89b96d","19d6a36b.8e41bd"]]},{"id":"133692dc.3646cd","type":"file","z":"553a6fa6.62e6d","name":"Where to go","filename":".node-red/node_modules/node-red-dashboard/dist/test.html","appendNewline":true,"createDir":false,"overwriteFile":"false","x":1143,"y":328,"wires":[]},{"id":"7a6903c9.162bac","type":"csv","z":"553a6fa6.62e6d","name":"","sep":",","hdrin":"","hdrout":"","multi":"one","ret":"\\n","temp":"","skip":"0","x":760,"y":280,"wires":[["75ea91a3.a354f"]]},{"id":"75ea91a3.a354f","type":"template","z":"553a6fa6.62e6d","name":"Convert to table","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"\n<table>\n <tr>\n  <th><p style=\"text-align:left;\"> <p style=\"color:white;\">Packet Captured </p></p></th>\n </tr>\n <tr>\n  <td><p style=\"text-align:left;\"> <p style=\"color:white;\">{{payload.col1}} </p></p></td>\n </tr>\n</table>\n","output":"str","x":950,"y":140,"wires":[["133692dc.3646cd"]]},{"id":"63a81deb.0647f4","type":"ui_button","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":0,"width":0,"height":0,"passthru":false,"label":"Clear Traffic Dump","color":"","bgcolor":"","icon":"","payload":" ","payloadType":"str","topic":"","x":90,"y":480,"wires":[["59b8eb03.2df414","acc93f1a.b16f3"]]},{"id":"59b8eb03.2df414","type":"file","z":"553a6fa6.62e6d","name":"Traffic Dump Clear","filename":".node-red/node_modules/node-red-dashboard/dist/test.html","appendNewline":true,"createDir":false,"overwriteFile":"true","x":650,"y":420,"wires":[]},{"id":"f0c4c1b9.a10d1","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"10","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"Traffic Dump Complete ","name":"","x":310,"y":160,"wires":[]},{"id":"765624b5.ac784c","type":"ping","z":"553a6fa6.62e6d","name":"8.8.8.8","host":"8.8.8.8","timer":"1","x":260,"y":60,"wires":[["6fce2b6c.bf27d4","6eead369.66c4fc"]]},{"id":"4b6c766f.8beab8","type":"ping","z":"553a6fa6.62e6d","name":"","host":"1.1.1.1","timer":"1","x":280,"y":120,"wires":[["78ef122a.5d202c","6fce2b6c.bf27d4"]]},{"id":"19d6a36b.8e41bd","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"30","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":180,"y":240,"wires":[["f0c4c1b9.a10d1"]]},{"id":"acc93f1a.b16f3","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"3","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":380,"y":520,"wires":[["d88b23a5.a588c"]]},{"id":"d88b23a5.a588c","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"3","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"Traffic Dump Deleted","name":"","x":563,"y":534,"wires":[]},{"id":"5d344050.4a942","type":"ui_group","z":"","name":"Default","tab":"1bedf069.d332","disp":false,"width":"7","collapse":false},{"id":"2b4d2ef5.e89192","type":"ui_group","z":"","name":"Configure IP","tab":"6c06e969.f1fec8","disp":true,"width":"6","collapse":false},{"id":"1bedf069.d332","type":"ui_tab","z":"","name":"Drop-Tap","icon":"dashboard","order":1},{"id":"6c06e969.f1fec8","type":"ui_tab","z":"","name":"Setting","icon":"settings","order":3}]
```
This should be imported from the menu located in the upper right and select Import + Clipboard after copying

![Import Menu  ](/assets/img/DropTapImages/Product/DropTap1.png)

Your window should now look like the following:

![Over View ](/assets/img/DropTapImages/Product/DropTap4.png)

If everything is completed you should now navigate your web browser to localhost:1880/ui which should look like the following:

![Over View ](/assets/img/DropTapImages/Product/DropTap5.png)

If the graphics do not populate ensure that the DropTap is connected to a network which is active, repeat the bridge step process if needed. You may need to establish a cronjob to do this after a reboot.

Now we need to establish your network monitor in the Node-Red code, select the two values below and adjust them as needed.

![Adjustment ](/assets/img/DropTapImages/Product/DropTap6.png)

This will ping a selected internal network device and a external network device to ensure you have communication, the DropTap will ping each connection once every second and will report the ping response time for basic network analysis.


Next you will want to change the TCPDUMP settings in the TCPDUMP node as shown below

![TCPDump Adjustment ](/assets/img/DropTapImages/Product/DropTap7.png)

The TCPDUMP is currently assigned for the following command

```bash
sudo tcpdump -n -i eth1 ip and not net 1.1.1.1 and not net 8.8.8.8 and not net 192.168.3.1 and not net 192.168.3.25
```

You will want to adjust this command to meet the new requirements for the Network Monitor. This is done to avoid reporting on DropTap traffic as the scope of the project does not care if the DropTap is visible on the network.

Once complete select the "Deploy" button and the Drop-Tap will rebuild with the changes Made.

![DEPLOY ](/assets/img/DropTapImages/Product/DropTap8.png)

# Getting Started with DropTap

Once the DropTap has been set up we need to connect it to a wire networked computer we wish to monitor. Connect the DropTap to a power source and allow it to boot up. Next we need to connect the DropTap to the original network cable into eth0. You will then take a network cable and attach it to the USB Ethernet plug and connect that back into the host, this will be eth1.

## Connecting your mobile device to DropTap

Make sure you have downloaded and loaded the DropTap application found in the [Software / Hardware Requirements.](/hardware/software_requirements.md)

Now we use a mobile device with the DropTap app and connect to the wireless network labeled DropTap. Assign this network a unique IP address, the one used in this example is 192.168.3.25. Any changes to this address must be reflected in the TCPDUMP command found in the installation guidelines. [Installation of Drop Tap](/installation.md)

```bash
sudo tcpdump -n -i eth1 ip and not net 1.1.1.1 and not net 8.8.8.8 and not net 192.168.3.1 and not net 192.168.3.25
```

Change the 192.168.3.25 to the address you selected.

## Running analytics

You can now poll 30 seconds worth of traffic captures to ensure that traffic is flowing correctly by pressing "Traffic Dump" as shown below within the mobile app.

![Traffic Dump  ](/assets/img/DropTapImages/Product/DropTap9.png)

Once 30 seconds are up you will recieve a menu pop up stating capture is compete, select the menu icon in the upper left and select "Traffic Dump View"

![Traffic Dump View  ](/assets/img/DropTapImages/Product/DropTapUI2.png)

Successful traffic captures will be visible now and should look somewhat similar to below.

![Traffic Dump View  ](/assets/img/DropTapImages/Product/DropTapUI4.png)

## Resetting device

If at any time you need to restart the Raspberry Pi select the menu icon in the upper left and select "Setting" to open up the administration menu.

![Traffic Dump View  ](/assets/img/DropTapImages/Product/DropTapUI2.png)

You can now reset the device by hitting the "reboot" button on the left

![Traffic Dump View  ](/assets/img/DropTapImages/Product/DropTapUI3.png)

---
layout: post
title: "CYBR 8480 Project Milestone 1: Establishing Environment"
date: 2018-04-11
excerpt: "Requirements are extremely important for conducting a successful project. these are the application requirements for the DropTap."
tags: [Environment, security, droptap, project]
feature: https://tap.apt-get-sudo.com/assets/img/environment.jpg
comments: true
---

# Establishing the Environment
This project utilizes Raspbian Stretch which is located https://downloads.raspberrypi.org/raspbian_latest

This project will utilize Node-Red which is located https://nodered.org/
This application is part of the Raspbian project
The Palette used in this project are:
node-red-Ping
node-red-dashboard

The Raspberry Pi needs to be utilized as a Network tap so the Ethernet network will be utilized for this purpose. We will utilize a USB Ethernet plug to complete this network bridge to establish our self on the Network.

## We will establish this bridge using the following command

 ```bash
brctl addbr br0
 ```

## Now we want to add eth0 to the bridge so we type to following command

```bash
brctl addif br0 eth0
```

## Now to add the USB network port to the bridge we conduct the following plug

```bash
brctl addif br0 eth1
```

## Now we need to prep the network connections, lets start with the eth0 and place it in promiscuous mode

```bash
ifconfig eth0 0.0.0.0 up promisc
```

## Ok and now lets do eth1 and place it in promiscuous node_modules

```bash
ifconfig eth1 0.0.0.0 up promisc
```

## Now lets put our Raspberry Pi as a man in the middle within the bridge

```bash
echo 8 > /sys/class/net/br0/bridge/group_fwd_mask
```
Now the environment is setup

## Now lets open up Node-red

```bash
node-red-start
```

Lets copy over the project file, copy the text below and place it on the input file

```JS
[{"id":"6fce2b6c.bf27d4","type":"ui_chart","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":1,"width":0,"height":0,"label":"Drop-Tap","chartType":"line","legend":"true","xformat":"auto","interpolate":"linear","nodata":"","dot":false,"ymin":"0","ymax":"","removeOlder":"100","removeOlderPoints":"100","removeOlderUnit":"1","cutout":0,"useOneColor":false,"colors":["#1f77b4","#aec7e8","#ff7f0e","#2ca02c","#98df8a","#d62728","#ff9896","#9467bd","#c5b0d5"],"useOldStyle":false,"x":699,"y":62,"wires":[[],[]]},{"id":"78ef122a.5d202c","type":"ui_gauge","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":2,"width":"6","height":"4","gtype":"gage","title":"Internal","label":"p/sec","format":"{{value}}","min":0,"max":"50","colors":["#00b500","#e6e600","#ca3838"],"seg1":"30","seg2":"40","x":692,"y":125,"wires":[]},{"id":"6eead369.66c4fc","type":"ui_gauge","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":3,"width":"6","height":"4","gtype":"gage","title":"External","label":"p/sec","format":"{{value}}","min":0,"max":"50","colors":["#00b500","#e6e600","#ca3838"],"seg1":"30","seg2":"40","x":691,"y":186,"wires":[]},{"id":"20f6f7c3.5bd7f8","type":"inject","z":"553a6fa6.62e6d","name":"","topic":"","payload":"","payloadType":"date","repeat":"","crontab":"","once":true,"x":230,"y":640,"wires":[["fdb97867.9c6dc8"]]},{"id":"fdb97867.9c6dc8","type":"exec","z":"553a6fa6.62e6d","command":"cat /etc/dhcpcd.conf","addpay":false,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":456,"y":639,"wires":[["a5d35868.c0f168"],[],[]]},{"id":"a5d35868.c0f168","type":"function","z":"553a6fa6.62e6d","name":"","func":"var lines = msg.payload.split(\"\\n\");\nvar data = [];\n\nfor(var i=0; i< lines.length; i++){\n    if(lines[i].indexOf(\"interface eth0\") != -1)\n        break;\n}\n\nif(i != lines.length){\n   for(i; i< lines.length; i++){\n        var tmp = lines[i].split(\"=\");\n        if(tmp.length==2){\n            var value = {};\n            value.text = tmp[0].trim();\n            value.payload = tmp[1].trim();\n            data.push(value);\n        }\n    } \n}\n\nif(data.length != 3)\n msg = null;\nelse\n msg = data;\n\n\n \nreturn msg;","outputs":"3","noerr":0,"x":707,"y":626,"wires":[["1495d323.c396dd"],["1495d323.c396dd"],["1495d323.c396dd","b4440167.5940e"]]},{"id":"1495d323.c396dd","type":"switch","z":"553a6fa6.62e6d","name":"","property":"text","propertyType":"msg","rules":[{"t":"eq","v":"static ip_address","vt":"str"},{"t":"eq","v":"static routers","vt":"str"},{"t":"eq","v":"static domain_name_servers","vt":"str"}],"checkall":"false","outputs":3,"x":886,"y":624,"wires":[["44b160be.5e5f4"],["1984f2cb.81f37d"],["1d93369d.ad03b9"]]},{"id":"b088bf7f.747ab","type":"ui_text_input","z":"553a6fa6.62e6d","name":"ip_address","label":"IP Address","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1217,"y":581,"wires":[["fd94e70.a4a0d18"]]},{"id":"a4d0b7e3.254958","type":"ui_text_input","z":"553a6fa6.62e6d","name":"router","label":"Router","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1196,"y":624,"wires":[["29596487.70e88c"]]},{"id":"29bbaa89.588376","type":"ui_text_input","z":"553a6fa6.62e6d","name":"dns","label":"DNS","group":"2b4d2ef5.e89192","order":0,"width":0,"height":0,"passthru":false,"mode":"text","delay":"0","topic":"","x":1196,"y":667,"wires":[["cd04d770.9b8b78"]]},{"id":"4a92297a.40a768","type":"exec","z":"553a6fa6.62e6d","command":"sudo sed -i ","addpay":true,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":1553,"y":622,"wires":[[],[],[]]},{"id":"44b160be.5e5f4","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"ip_address\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":1067.5,"y":581,"wires":[["b088bf7f.747ab"]]},{"id":"1984f2cb.81f37d","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"router\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":1066,"y":624,"wires":[["a4d0b7e3.254958"]]},{"id":"1d93369d.ad03b9","type":"function","z":"553a6fa6.62e6d","name":"","func":"flow.set(\"dns\", msg.payload);\nreturn msg;","outputs":1,"noerr":0,"x":1069,"y":667,"wires":[["29bbaa89.588376"]]},{"id":"fd94e70.a4a0d18","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static ip_address={{flow.ip_address}}/static ip_address={{payload}}/g;' /etc/dhcpcd.conf","x":1377.5,"y":581,"wires":[["4a92297a.40a768"]]},{"id":"29596487.70e88c","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static routers={{flow.router}}/static routers={{payload}}/g;' /etc/dhcpcd.conf","x":1376,"y":624,"wires":[["4a92297a.40a768"]]},{"id":"cd04d770.9b8b78","type":"template","z":"553a6fa6.62e6d","name":"","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"'s/static domain_name_servers={{flow.dns}}/static domain_name_servers={{payload}}/g;' /etc/dhcpcd.conf","x":1375,"y":667,"wires":[["4a92297a.40a768"]]},{"id":"63a7f97e.0afe28","type":"link in","z":"553a6fa6.62e6d","name":"","links":[],"x":281.5,"y":582,"wires":[["fdb97867.9c6dc8"]]},{"id":"c87a8a93.7cac08","type":"ui_button","z":"553a6fa6.62e6d","name":"reboot","group":"2b4d2ef5.e89192","order":0,"width":"3","height":"1","passthru":false,"label":"Reboot","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":276.6666564941406,"y":788.5555686950684,"wires":[["230d077b.ee6328"]]},{"id":"230d077b.ee6328","type":"exec","z":"553a6fa6.62e6d","command":"sudo reboot","addpay":false,"append":"","useSpawn":"","timer":"","oldrc":false,"name":"","x":487.22217178344727,"y":788.8888463973999,"wires":[[],[],[]]},{"id":"648b2feb.35d34","type":"ui_button","z":"553a6fa6.62e6d","name":"refresh","group":"2b4d2ef5.e89192","order":0,"width":"3","height":"1","passthru":false,"label":"Refresh","color":"","bgcolor":"","icon":"","payload":"true","payloadType":"bool","topic":"","x":91.44442749023438,"y":707.332911491394,"wires":[["39749098.adc83"]]},{"id":"4998eff1.1e7f1","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"3","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"","name":"","x":1052.777744293213,"y":798.5553007125854,"wires":[]},{"id":"b4440167.5940e","type":"change","z":"553a6fa6.62e6d","name":"","rules":[{"t":"set","p":"payload","pt":"msg","to":"","tot":"str"}],"action":"","property":"","from":"","to":"","reg":false,"x":915.5554542541504,"y":717.4442138671875,"wires":[["4998eff1.1e7f1"]]},{"id":"39749098.adc83","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"300","timeoutUnits":"milliseconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":258.8888740539551,"y":707.4445114135742,"wires":[["fdb97867.9c6dc8"]]},{"id":"16267357.89b96d","type":"exec","z":"553a6fa6.62e6d","command":"sudo tcpdump -n","addpay":false,"append":"","useSpawn":"true","timer":"10","oldrc":false,"name":"","x":380,"y":360,"wires":[["7a6903c9.162bac"],[],[]]},{"id":"2eff459a.0c6a8a","type":"ui_button","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":0,"width":0,"height":0,"passthru":false,"label":"Traffic Dump","color":"","bgcolor":"","icon":"","payload":"","payloadType":"str","topic":"","x":120,"y":380,"wires":[["16267357.89b96d","19d6a36b.8e41bd"]]},{"id":"133692dc.3646cd","type":"file","z":"553a6fa6.62e6d","name":"Where to go","filename":".node-red/node_modules/node-red-dashboard/dist/test.html","appendNewline":true,"createDir":false,"overwriteFile":"false","x":1143,"y":328,"wires":[]},{"id":"7a6903c9.162bac","type":"csv","z":"553a6fa6.62e6d","name":"","sep":",","hdrin":"","hdrout":"","multi":"one","ret":"\\n","temp":"","skip":"0","x":760,"y":280,"wires":[["75ea91a3.a354f"]]},{"id":"75ea91a3.a354f","type":"template","z":"553a6fa6.62e6d","name":"Convert to table","field":"payload","fieldType":"msg","format":"handlebars","syntax":"mustache","template":"\n<table>\n <tr>\n  <th><p style=\"text-align:left;\"> <p style=\"color:white;\">Packet Captured </p></p></th>\n </tr>\n <tr>\n  <td><p style=\"text-align:left;\"> <p style=\"color:white;\">{{payload.col1}} </p></p></td>\n </tr>\n</table>\n","output":"str","x":950,"y":140,"wires":[["133692dc.3646cd"]]},{"id":"63a81deb.0647f4","type":"ui_button","z":"553a6fa6.62e6d","name":"","group":"5d344050.4a942","order":0,"width":0,"height":0,"passthru":false,"label":"Clear Traffic Dump","color":"","bgcolor":"","icon":"","payload":" ","payloadType":"str","topic":"","x":140,"y":460,"wires":[["59b8eb03.2df414","acc93f1a.b16f3"]]},{"id":"59b8eb03.2df414","type":"file","z":"553a6fa6.62e6d","name":"Traffic Dump Clear","filename":".node-red/node_modules/node-red-dashboard/dist/test.html","appendNewline":true,"createDir":false,"overwriteFile":"true","x":650,"y":420,"wires":[]},{"id":"f0c4c1b9.a10d1","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"10","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"Traffic Dump Complete ","name":"","x":310,"y":160,"wires":[]},{"id":"765624b5.ac784c","type":"ping","z":"553a6fa6.62e6d","name":"","host":"8.8.8.8","timer":"1","x":260,"y":60,"wires":[["6fce2b6c.bf27d4","6eead369.66c4fc"]]},{"id":"4b6c766f.8beab8","type":"ping","z":"553a6fa6.62e6d","name":"","host":"1.1.1.1","timer":"1","x":280,"y":120,"wires":[["78ef122a.5d202c","6fce2b6c.bf27d4"]]},{"id":"19d6a36b.8e41bd","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"30","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":180,"y":240,"wires":[["f0c4c1b9.a10d1"]]},{"id":"acc93f1a.b16f3","type":"delay","z":"553a6fa6.62e6d","name":"","pauseType":"delay","timeout":"5","timeoutUnits":"seconds","rate":"1","nbRateUnits":"1","rateUnits":"second","randomFirst":"1","randomLast":"5","randomUnits":"seconds","drop":false,"x":380,"y":520,"wires":[["d88b23a5.a588c"]]},{"id":"d88b23a5.a588c","type":"ui_toast","z":"553a6fa6.62e6d","position":"top right","displayTime":"3","highlight":"","outputs":0,"ok":"OK","cancel":"","topic":"Traffic Dump Deleted","name":"","x":620,"y":540,"wires":[]},{"id":"5d344050.4a942","type":"ui_group","z":"","name":"Default","tab":"1bedf069.d332","disp":false,"width":"7","collapse":false},{"id":"2b4d2ef5.e89192","type":"ui_group","z":"","name":"Configure IP","tab":"6c06e969.f1fec8","disp":true,"width":"6","collapse":false},{"id":"1bedf069.d332","type":"ui_tab","z":"","name":"Drop-Tap","icon":"dashboard","order":1},{"id":"6c06e969.f1fec8","type":"ui_tab","z":"","name":"Setting","icon":"settings","order":3}]
```
You environment should now look like this

![Overall DropTap UI  ](/assets/img/DropTapImages/Product/DropTapUIDev1.png)

When you navigate to the Raspberry Pi from your mobile device you will find the following Interface

![Overall DropTap UI mobile ](/assets/img/DropTapImages/Product/DropTapUI1.png)

There are three unique settings available to the user which include Drop Tap, Traffic Capture and the settings page which looks like the following

![Overall DropTap UI sections ](/assets/img/DropTapImages/Product/DropTapUI2.png)

The settings available allow the user to change the IP address and reboot the device from the mobile device

![Overall DropTap UI settings ](/assets/img/DropTapImages/Product/DropTapUI3.png)

The traffic dump needs to be initiated from the Drop Tap menu and can be visible in this window which now looks like the following 30 sec traffic capture

![Overall DropTap UI mobile ](/assets/img/DropTapImages/Product/DropTapUI4.png)

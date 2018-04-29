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

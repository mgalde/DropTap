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

The DropTap also makes use of a mobile application titled DropTap which pulls the relevant information when connected to the DropTap network. The application can be found [HERE. ](/assets/app/DropTap.apk)

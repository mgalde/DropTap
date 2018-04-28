# Drop Tap Installation

It is important to note that the DropTap platform has been tested and developed to work with the materials found within [the Hardware Requirements](/hardware/software_requirements.md), any additional materials that deviate from this list may need additional steps.

## Establishing a base system

First step is to write the [Raspbian image ](https://downloads.raspberrypi.org/raspbian_latest) onto your [SD card ](https://www.amazon.com/Sandisk-Ultra-Micro-UHS-I-Adapter/dp/B073JWXGNT)and place it within your Raspberry Pi. This is accomplished by using a program like [Etcher ](https://etcher.io/)which is what was used to create the image for DropTap.

Once you boot into the Raspberry Pi you need to connect your [Ethernet Adapter ](https://www.amazon.com/AmazonBasics-1000-Gigabit-Ethernet-Adapter/dp/B00M77HMU0)which will be assigned eth1. This will be needed to establish the bridge.

### We will establish this bridge using the following command

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

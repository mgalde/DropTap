# DropTap

This project is also visible from https://tap.apt-get-sudo.com

## User stories
As a **Network Administrator**, I want to **remotely access my network traffic from my mobile device** so I can **save time by not needing to be at a work station**.
**Acceptance Criteria:**
* Network administrator will be able to conduct basic network diagnostics utilizing the users mobile device and the DropTap
* The network administrator will be able to deploy the DropTap and not need to do any additional configuration

As a **Network Technician**, I want to **be able to verify network devices I am connecting together are communicating** so I can **verify communication is successful and not need to further diagnose**.
**Acceptance Criteria:**
* Network technician will utilize a DropTap during a device install to verify that communication is taking place to the device on the Network
* Network technician will utilize the DropTap to see what traffic is flowing between the new device and connected devices
* Network technician will utilize the DropTap to preform basic network diagnostics to include ping and trace route requests

As a **Help Desk Support**, I want to **monitor network traffic at various points** so I can **identify what nodes are operational or offline**.
**Acceptance Criteria:**
* Help desk will be able to utilize deployed DropTap devices to test the network from a remote location to verify if a site it down or notifications
* Help desk will be able to poll deployed DropTap devices to take general network health from a enterprise network and be notified of network interruptions

## Misuser stories
As a **malicious actor**, I want to **deploy a DropTap on a unsuspecting network** so I can **capture network traffic I should not have access to**.
**Mitigations:**
* Mitigation technique 1 will be to set a easy to understand hostname that will identify the DropTap during a network scan
* Mitigation technique 2 will create a announcement packet which will broadcast before a capture as a packet that can be intercepted during a network scan

As a **malicious actor**, I want to **compromise a legitimate DropTap** so I can **have a easy way into the network**.
**Mitigations:**
* Mitigation technique 1 will be to set a authentication portal for the DropTap admin portal
* Mitigation technique 2 will harden the Raspberry Pi through closing ports and stopping services not needed for the DropTap service
* Mitigation technique 3 will securely connect the DropTap to a authenticated mobile user to limit the attack surface

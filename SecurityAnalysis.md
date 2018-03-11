## Security analysis DropTap connections
The DropTap is a Raspberry Pi 3 with a USB network dongle which will bridge a connection between a device and its end point. The device can be inserted into a unsuspecting network or within a malicious network which will need mitigation.
![Overall DropTap Overview ](/assets/img/DropTapImages/DropTap1.jpeg)

| Component name | Category of vulnerability | Issue Description | Mitigation |
|----------------|---------------------------|-------------------|------------|
| Network cable attached to DropTap and source | Malicious traffic evasion | This component exposes a additional hop between source and destination, A attacker could use this additional hop to attempt to hide malicious traffic | The DropTap will utilize a bridge network which should not be noticeable from the source or destination components .|
| Network cable attached to DropTap and original input | Malicious traffic evasion | This component exposes a additional hop between source and destination, A attacker could use this additional hop to attempt to hide malicious traffic | The DropTap will utilize a bridge network which should not be noticeable from the source or destination components .|


## Security analysis DropTap UI
The DropTap is a Raspberry Pi 3 with a mobile device for user interaction. The Raspberry pi it self is hosting a web service that the user connects to
![Overall DropTap UI Concept ](/assets/img/DropTapImages/DropTap2.jpeg)

| Component name | Category of vulnerability | Issue Description | Mitigation |
|----------------|---------------------------|-------------------|------------|
| Packet capture interface basic network tools | Network DoS | This component exposes a potential ability to exceed network traffic to various services from within a network and potentially degrade performance  | The DropTap will utilize a hardcoded network limit of how many packets it will be capable of sending while in passive mode .|
| Packet capture interface Packet Capture list | Sensitive data exfiltration | This component exposes exit node for captured packets, a rogue DropTap could be inserted into a network and all traffic can be sent to a malicious user | The DropTap will utilize live traffic capture with no PCAPS or packet storage capabilities  .|


## Security analysis DropTap Hardware
The DropTap is a Raspberry Pi 3 with a mobile device for user interaction. The Raspberry Pi will utilize a network adapter to enable a network bridge
![Overall DropTap Hardware Concept ](/assets/img/DropTapImages/DropTap3.jpeg)

| Component name | Category of vulnerability | Issue Description | Mitigation |
|----------------|---------------------------|-------------------|------------|
| Raspberry Pi Wifi | Network DoS | This component exposes a potential ability deny service on expected wifi channels  | The DropTap will utilize all available techniques to provide a stable connection to the mobile user when possible .|

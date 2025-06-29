---
up: 
created: 2025-01-10
tags:
---
The GUI client can only be installed using Mac App Store (`mas`).
Use ⌘ N to add a new empty tunnel.

![[WireGuard MacOS Client.png]]

Once created, the tunnel's configuration can be edited:
```
[Interface]
PrivateKey = <auto-created-private-ip>
Address = 192.168.33.50/32

[Peer]
PublicKey = 55d24+7dL8eyQN8rvXfVy/q15I6TFN0thb0rBWbFTAo=
AllowedIPs = 192.168.33.0/24, 192.168.1.0/24
Endpoint = <wireguard-server-domain-or-ip>:51820
```
If we are setting up a VPN tunnel to gain remote access to a LAN network, `AllowedIps` should be all the subnets that the client could gain access to, in addition to the designated VPN subnet (192.168.33.0/24 in this example).

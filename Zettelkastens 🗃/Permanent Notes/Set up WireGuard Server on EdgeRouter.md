---
up:
  - "[[Wireguard MOC]]"
  - "[[EdgeRouter MOC]]"
created: 2025-01-10
tags:
---
[[What is WireGuard|WireGuard is simple and fast modern VPN that utilize state-of-the-art cryptography]]. A traditional VPN tunneling architecture with WireGuard involves a WireGuard Server.
## Prerequisite
Know how to execute commands in EdgeRouter CLI.
## Instruction
### Download WireGuard
WireGuard Debian package for EdgeRouter OS (EdgeOS) is hosted at [Github release page](https://github.com/WireGuard/wireguard-vyatta-ubnt/releases/latest). We can use `curl` to download the package inside WireGuard CLI:
```bash
curl -OL https://github.com/WireGuard/wireguard-vyatta-ubnt/releases/download/${RELEASE}/${BOARD}-${RELEASE}.deb
```
with `BOARD` corresponding to the model of the EdgeRouter as described in the release page.
### Install WireGuard
Simply using `dpkg` to install the `deb` package:
```bash
sudo dpkg -i ${BOARD}-${RELEASE}.deb
```
### Configure interfaces
A WireGuard connection require both ends (also known as "peers") to trust each other via asymmetric key exchange. As a result, in order to set up a WireGuard server, we need to generate public and private keys:
```bash
wg genkey | tee /config/auth/wg.key | wg pubkey > /config/auth/wg.public
```
We can then configure a virtual `wg0` interface for the VPN connection:
```bash
configure

set interfaces wireguard wg0 address 192.168.33.1/24
set interfaces wireguard wg0 listen-port 51820
set interfaces wireguard wg0 route-allowed-ips true
set interfaces wireguard wg0 private-key /config/auth/wg.key

commit; save
exit
```
### Set up Firewall rules
We need to add an `WAN_LOCAL` EdgeRouter Firewall rule to accept incoming UDP traffic destined for the WireGuard server’s port.
```bash
configure

set firewall name WAN_LOCAL rule 30 action accept
set firewall name WAN_LOCAL rule 30 protocol udp
set firewall name WAN_LOCAL rule 30 description 'WireGuard'
set firewall name WAN_LOCAL rule 30 destination port 51820

commit; save
exit
```
**Related:** [[Manage Firewall on EdgeRouter]]
## Managing peers
Before configuring peers in the router, we need to set up WireGuard Client on those "peers". For example, [[Set up MacOS WireGuard Client]].
Peers can be then added using the CLI:
```bash
configure

set interfaces wireguard wg0 peer GIPWDet2eswjz1JphYFb51sh6I+CwvzOoVyD7z7kZVc= endpoint example1.org:29922
set interfaces wireguard wg0 peer GIPWDet2eswjz1JphYFb51sh6I+CwvzOoVyD7z7kZVc= allowed-ips 192.168.33.101/32
set interfaces wireguard wg0 peer GIPWDet2eswjz1JphYFb51sh6I+CwvzOoVyD7z7kZVc= description "peer 1"

commit; save
exit
```
The `endpoint` setting is optional and should only be configured if the peer does have a public IP address (for example, another router in a remote location).
## References
- The official documentation of the EdgeOS WireGuard Package at [Github](https://github.com/WireGuard/wireguard-vyatta-ubnt/wiki/EdgeOS-and-Unifi-Gateway).
- A blog post at [netsparse.dev](https://netsparse.dev/posts/2023-03/setup-wireguard-edgerouter/).

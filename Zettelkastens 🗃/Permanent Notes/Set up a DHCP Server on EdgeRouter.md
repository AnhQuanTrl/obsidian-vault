---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-10
tags:
---
Enter configuration mode:
```
configure
```
*(Optional)* If the `dhcp-server` service is not enabled (which is highly unlikely), enable it:
```
set service dhcp-server disabled false
```
Set up an authoritative DHCP server
```
set service dhcp-server shared-network-name EMERGENCY authoritative enable  
set service dhcp-server shared-network-name EMERGENCY subnet 192.168.2.0/24 default-router 192.168.2.1  
set service dhcp-server shared-network-name EMERGENCY subnet 192.168.2.0/24 dns-server 192.168.2.1  
set service dhcp-server shared-network-name EMERGENCY subnet 192.168.2.0/24 lease 86400  
set service dhcp-server shared-network-name EMERGENCY subnet 192.168.2.0/24 start 192.168.2.38 stop 192.168.2.243
```
By default, the EdgeRouter's DHCP server uses the ISC DHCP daemon (DHCPD) as DNS server. To switch to `dnsmasq`, follow [[Turn on Dnsmasq for EdgeRouter DHCP server]].
## References
- Official documentation at [help.ui.com](https://help.ui.com/hc/en-us/articles/204952254-EdgeRouter-DHCP-Server).
---
up: 
created: 2025-01-11
tags:
---
```
set firewall group network-group LAN_NETWORKS description 'RFC1918 ranges'  
set firewall group network-group LAN_NETWORKS network 192.168.0.0/16  
set firewall group network-group LAN_NETWORKS network 172.16.0.0/12  
set firewall group network-group LAN_NETWORKS network 10.0.0.0/8
```
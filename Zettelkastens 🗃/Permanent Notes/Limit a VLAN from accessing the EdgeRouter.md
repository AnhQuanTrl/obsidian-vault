---
up: 
created: 2025-01-14
tags:
---
Use a `LOCAL` direction firewall ruleset for this use-case.
```
set firewall name GUEST_LOCAL default-action drop
set firewall name GUEST_LOCAL description 'guest to router'

set interfaces switch switch0 vif 30 firewall local name GUEST_LOCAL
```
The VLAN obviously still needs to access the router's DNS and DHCP services. 
```
set firewall name GUEST_LOCAL rule 10 action accept  
set firewall name GUEST_LOCAL rule 10 description 'allow dns'  
set firewall name GUEST_LOCAL rule 10 log disable  
set firewall name GUEST_LOCAL rule 10 protocol tcp_udp  
set firewall name GUEST_LOCAL rule 10 destination port 53  
  
set firewall name GUEST_LOCAL rule 20 action accept  
set firewall name GUEST_LOCAL rule 20 description 'allow dhcp'  
set firewall name GUEST_LOCAL rule 20 log disable  
set firewall name GUEST_LOCAL rule 20 protocol udp  
set firewall name GUEST_LOCAL rule 20 destination port 67
```
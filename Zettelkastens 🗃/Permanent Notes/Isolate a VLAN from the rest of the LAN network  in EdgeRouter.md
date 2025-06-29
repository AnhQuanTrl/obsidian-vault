---
up: 
created: 2025-01-11
tags:
---
Enter configuration mode.

At first, define a network group that encompass all private subnets (see [[Add an network group on EdgeRouter]]):
- 192.168.0.0/16  
- 172.16.0.0/12  
- 10.0.0.0/8

To prevent a VLAN from accessing other VLANs and subnets, configure `IN` direction firewall rules on the VLAN’s network interface:
```
set firewall name GUEST_IN default-action accept   
set firewall name GUEST_IN description 'guest to lan/wan'

set interfaces switch0 vif 30 firewall in name GUEST_IN
```

> [!warning]
> It is important that the default action is `accept` so that the VLAN can still access the Internet.

This rule allows other network to still be able to access the isolated network.
```
set firewall name GUEST_IN rule 10 action accept  
set firewall name GUEST_IN rule 10 description 'Allow established/related'  
set firewall name GUEST_IN rule 10 state established enable  
set firewall name GUEST_IN rule 10 state related enable
```

> [!info]
> `Allow established/related` should always be the first rule.

Then, define a rule that drop all traffic to the network group defined earlier:
```
set firewall name GUEST_IN rule 20 action drop  
set firewall name GUEST_IN rule 20 description 'drop guest to lan'  
set firewall name GUEST_IN rule 20 destination group network-group LAN_NETWORKS  
set firewall name GUEST_IN rule 20 protocol all
```

> [!tip]
> We can override this `drop-all` rule for some traffic by inserting some `accept` rules before it. This is because EdgeRouter evaluates the firewall rules from lowest order to highest order and immediately stops once a rule is matched.

For stricter security, refer to [[Limit a VLAN from accessing the EdgeRouter]].
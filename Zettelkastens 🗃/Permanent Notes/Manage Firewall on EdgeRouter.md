---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-11
tags:
---
Firewall in EdgeRouter is managed using Firewall Ruleset. A ruleset is basically just a bunch of rules that either allow or drop traffic coming into an interface. 
We can set some basic options for a ruleset such as its name, default action, and description:
```bash
set firewall name GUEST_IN default-action accept   
set firewall name GUEST_IN description 'guest to lan/wan'
set firewall name GUEST_LOCAL default-action drop  
set firewall name GUEST_LOCAL description 'guest to router'
```
**Anatomy of a firewall rule**:
- rule order: rules are processed from lowest to highest.
- description.
- protocol: network procotol.
- destination: limiting the destinations that this rule applies.
- action: accept or drop.
- log: whether to enable firewall logging. 

Some firewall rules examples:
- Denying traffic to the whole LAN networks except a webserver.
```
set firewall name GUEST_IN rule 10 action accept  
set firewall name GUEST_IN rule 10 description 'allow webserver'  
set firewall name GUEST_IN rule 10 protocol tcp  
set firewall name GUEST_IN rule 10 destination address 192.168.1.10  
set firewall name GUEST_IN rule 10 destination port 80,443  
  
set firewall name GUEST_IN rule 20 action drop  
set firewall name GUEST_IN rule 20 description 'drop guest to lan'  
set firewall name GUEST_IN rule 20 destination group network-group LAN_NETWORKS  
set firewall name GUEST_IN rule 20 protocol all
```

> [!tip]
> As we can see, a destination can be a group of subnets called `network-group`. We can [[Add an network group on EdgeRouter]] to ease the maintenance effort of creating firewall rules.

- [[Isolate a VLAN from the rest of the LAN network  in EdgeRouter]].
- 

A firewall ruleset needs to be attached to a network interface (whether it is physical or virtual) for **one** single *direction*: IN (for network entering the interface), OUT (for network exiting the interface) and LOCAL (for network destined for the router itself from the interface).
```bash
set interfaces ethernet eth2 firewall in name GUEST_IN  
set interfaces ethernet eth2 firewall local name GUEST_LOCAL
```
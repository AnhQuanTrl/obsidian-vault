---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-10
tags:
---
Enter Configuration mode.
```bash
configure
```
Enable VLAN-aware switch on `switch0` interface:
```bash
set interfaces switch switch0 switch-port vlan-aware enable
```
Add a VLAN interface (VIF) to `switch0`:
```bash
set interfaces switch switch0 vif 10 address 10.0.10.1/24
set interfaces switch switch0 vif 10 description "Guest"
```
Afterward, [[Set up a DHCP Server on EdgeRouter]] for the subnet associated with the newly added VLAN.

Once done, start assigning `switch0`'s child interfaces (`ethX`) to the VLANs.
```
set interfaces switch switch0 switch-port interface eth4 vlan pvid 10  
set interfaces switch switch0 switch-port interface eth4 vlan vid 20
```

> [!tip]
> An untagged VLAN is defined with the **pvid** value, whereas a tagged VLAN is defined with **vid**.

*(optional if VLAN is allowed to reach the Internet)* Make sure to [[Manage DNS forwarding on EdgeRouter]], especially adding the VLAN interface (which is named as `<parent-interface>.<vif>`, for example `switch0.10`) to the DNS forwarding `listen-on` interfaces. 
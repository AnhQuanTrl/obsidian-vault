---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-10
tags:
---
Before setting up VLAN, it is important that we designate a port on the router for Emergency access. If we are using an EdgeRouter model with a virtual switch interface `switch0`, the first step is to remove an ethernet interface from the `switch0` interface: [[Manage virtual switch0 interface of EdgeRouter X]].

Once a spare physical port is chosen, assign the corresponding interface its own subnet, **different from any other local subnet.** Afterward, [[Set up a DHCP Server on EdgeRouter]] for that subnet.


---
up:
  - "[[Proxmox MOC]]"
created: 2025-01-12
tags:
---
A VLAN-aware virtual bridge allows us to assign different VLANs to individual VMs, enhancing security.
## Prerequisite
Make sure that all the VLANs that are managed by this virtual bridge to be **Tagged**.
## Instruction
Convert the current virtual bridge settings to be VLAN-aware:
```
auto vmbr0
iface vmbr0 inet manual
        bridge-ports eno1
        bridge-stp off
        bridge-fd 0
        bridge-vlan-aware yes
        bridge-vids 2-4094
```

Next, assign a VLAN tag to a VM as follows:
![[VLAN Tag in Proxmox.png]]
*Optionally*, we can use a VLAN from the virtual bridge for the Proxmox VE management IP address:
```
auto vmbr0.100
iface vmbr0.100 inet static
        address 10.0.100.4/24
        gateway 10.0.100.1
```

Finally, [[Reload networking settings in Proxmox]].

> [!warning]
> Don't forget about [[Steps to re-configure after changing a Proxmox node's management IP address]].

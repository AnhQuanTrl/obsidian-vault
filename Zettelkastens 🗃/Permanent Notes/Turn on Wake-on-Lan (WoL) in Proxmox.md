---
up:
  - "[[Proxmox MOC]]"
created: 2025-01-12
tags:
---
To turn on Wake-on-Lan for Proxmox server, first we need to [[Turn on WoL setting in the BIOS]]. 
Once the BIOS setting is configured, [[Enable WoL on the network adapter in Linux]].

For Proxmox, the process of making WoL persistent differs slightly from standard methods. The `/etc/network/interfaces` file needs to be edited with an extra `post-up` line in the interface section. For example:
```
auto vmbr0
iface vmbr0 inet manual
        bridge-ports eno1
        bridge-stp off
        bridge-fd 0
        bridge-vlan-aware yes
        bridge-vids 2-4094
        post-up /sbin/ethtool -s <physical-interface> wol g
```

> [!warning]
> `<physical-interface>` must be a physical network interface on the proxmox host such as `eno1`. 
> 

> [!tip]
> The `post-up` line can be added to other network interfaces, not just virtual bridges like `vmbr0`, as long as the network interface is configured for Autostart (denoted by `auto` line in `/etc/network/interfaces` file).

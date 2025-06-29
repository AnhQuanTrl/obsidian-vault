---
up: 
created: 2025-01-12
tags:
---
To query the status of this setting, use `ethtool`:
```
ethtool <interface> | grep Wake-on
```
`interface` can be looked up by using `ip address` command. 

Example output of this command:
```
Supports Wake-on: pumbg
Wake-on: d
```
If Wake-on is already `g`, this means that the network driver has WoL switched on by default. 

Otherwise, use
```
ethtool -s <interface> wol g
```
to switch on the feature.

Once done, [[Make WoL persistent between reboots]].

## References
- [ArchLinux documentation about Wake-on-Lan](https://wiki.archlinux.org/title/Wake-on-LAN).
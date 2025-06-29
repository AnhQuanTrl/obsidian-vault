---
up: 
created: 2025-01-12
tags:
---
1. Update the `/etc/hosts` file or Node > System > Hosts in the web interface. Change the old IP address corresponding with the Proxmox node's FQDN.
```
10.0.100.5 pve2.arthurtran.dev pve2
```
2. Update the DNS server manually in Node > System > DNS to the new default gateway.
3. Update node certificates (force creating new):
```
pvecm updatecerts -f
```
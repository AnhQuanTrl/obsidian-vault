---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-11
tags:
---
Modifying the cache size:
```bash
set service dns forwarding cache-size <nr>
```

Defining listening interface:
```bash
set service dns forwarding listen-on <interface>
```
If interface is empty, DNS forwarding will listen on all interfaces.
We can use:
```bash
set service dns forwarding except-interface <interface>
```
to set a black list instead of white list.

DNS forwarding on EdgeRouter is owned by a service called `dnsmasq`. This service will forward DNS requests to the specified DNS servers and cache the domain information for subsequent requests.
Most of the time, EdgeRouter obtain information about those upstream DNS servers from the ISP. We can manually override these name servers: [[Manage name servers on EdgeRouter]].




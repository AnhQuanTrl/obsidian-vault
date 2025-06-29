---
up:
  - "[[EdgeRouter MOC]]"
created: 2025-01-10
tags:
---
In this document, CloudFlare will be used as an example to represent a custom DNS provider.
## Prerequisite
An `A` DNS record needs to be set up that temporarily points to a random IP in CloudFlare. 
![[CloudFlare A Record for DDNS.png]]The Cloudflare Proxy feature should be enabled for domains using ports 80 and 443, and disabled for all other ports.
## Instruction
If the EdgeRouter WAN port is configured with PPPoE, replace `eth0` with the interface `pppoe0` for all the instructions in this section.

Enter configuration mode: 
```bash
configure
```
We begin with setting custom the dynamic DDNS hostname. We can repeat this step multiple time for each dynamic sub-domains.
```bash
set service dns dynamic interface eth0 service custom-cloudflare host-name <subdomain.domain.com>
```

> [!tip]
> The service name must start with `custom-`, unless configuring a built-in DDNS service.

Next, define the credentials used to update the DNS record:
```bash
set service dns dynamic interface eth0 service custom-cloudflare login <user@domain.com>  
set service dns dynamic interface eth0 service custom-cloudflare password <cloudflare-api-key>
```
Define the DNS dynamic protocol:
```bash
set service dns dynamic interface eth0 service custom-cloudflare protocol cloudflare
```
Finally, we need to specify the DNS zone that host the sub-domain. This step is needed for some protocols such as `cloudflare`.
```bash
set service dns dynamic interface eth0 service custom-cloudflare options zone=domain.com
```

> [!warning]
> Don't forget to commit and save!
## References
- Official documentation at [help.ui.com](https://help.ui.com/hc/en-us/articles/204976324-EdgeRouter-Custom-Dynamic-DNS).
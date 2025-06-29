---
up: 
created: 2025-01-11
tags:
---
If the internet connection configured in the onboard **Basic Setup** wizard is `dhcp`, EdgeRouter will automatically option the upstream DNS servers using DHCP: 
```
set service dns forwarding dhcp <interface>
```
We can manually override the DNS servers by executing:
```
set service dns forwarding name-server <ip-address>
```

If the Internet type is `pppoe`, DNS information will be obtained using PPPoE protocol. 
To override the DNS servers, first we need to turn off `pppoe` name-servers:
```
set interfaces ethernet eth0 pppoe 0 name-server none
```
Then, change the DNS servers in the system setting and switch DNS forwarding to `system` mode:
```
set service dns forwarding system  
set system name-server <ip-address>
```

> [!tip]
> Use these commands to show DNS forwarding name-servers and statistics:
> ```
> show dns forwarding nameservers  
> show dns forwarding statistics
> ```

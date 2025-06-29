---
up:
  - "[[Proxmox MOC]]"
created: 2025-01-14
tags:
---
Using CLI, we can create a cluster and join nodes togerther.
Starting with the first node:
```
pvecm create CLUSTERNAME
```
On another node, join it with the existing cluster:
```
pvecm add IP-ADDRESS-CLUSTER
```
with `IP-ADDRESS-CLUSTER` being the IP address of an existing node in the cluster.

> [!error] Critical
> Must ensure that number of nodes are odd.

If the number of nodes are not odd number, consider [[Add a Quorum Device to existing Proxmox cluster]].
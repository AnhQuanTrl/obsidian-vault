---
up: 
created: 2025-01-14
tags:
---
We will use a Raspberry Pi as an example.
Make sure that root SSH access is enabled:
```
echo "PermitRootLogin yes" | tee /etc/ssh/sshd_config.d/root_login.conf >/dev/null && systemctl restart ssh.service
```
Setup a password for the root account:
```
sudo passwd
```

Install package `corosync-qnetd` for the QDevice:
```
apt install corosync-qnetd

```
Install package `apt install corosync-qdevice` for all existing cluster nodes:
```
apt install corosync-qdevice
```

From an existing Proxmox node, execute the following command:
```
pvecm qdevice setup <QDEVICE-IP>
```
to add the QDevice to the cluster.
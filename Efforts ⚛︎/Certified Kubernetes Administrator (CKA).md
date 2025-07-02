---
up: 
created: 2024-12-11
rank: 2
tags:
  - effort/on
---
## Readiness checks


## Exam Notes

Use this to view kubelet configuration
```
ps aux | grep kubelet
```

Check kube-apiserver enabled admissions plugin, 
```
k exec kube-apiserver-controlplane -n kube-system -- kube-apiserver -h | grep enable-admission-plugins (or )
cat /etc/kubernetes/manifests | grep enable-admission-plugins
```
Use this to watching control plane pods after static manifests changed:
```
watch crictl ps
```

Kubeadm:
If forget the token after kubeadm init, create a new token using
```
 kubeadm token create --print-join-command
```

`.vimrc`
```
`set et # expandtab (use space character when tab key used) *`  
`set ts=2 # tabstop *`  
`set sw=2 # shiftwidth *`  
`set sts=2 # softtabstop (Let backspace delete indent **`  
`set ai # autoindent (Indent at the same level of the previous line)`  
`set si # smart indent`  
`set hls # highlightsearch (Highlight search terms)`  
`set ic # ignorecase when searching in vim`  
`set bg=dark # Assume a dark background (better color scheme)`  
`set nu # show line numbers`  
`syntax on # syntax highlighting`

`* preconfigured in the exam environment`  
`** minimum nice to have`
```

Things to remember:
```
lsmod | grep br_netfilter
cat <<EOF | sudo tee /etc/modules-load.d/k8s.conf
br_netfilter
overlay
EOF
sudo modprobe br_netfilter overlay

cat <<EOF | sudo tee /etc/sysctl.d/99-k8s.conf
net.ipv4.ip_forward = 1
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF

sudo sysctl --system
```

```
awk '{print $2}'
```

`Use :Exp to go back to netrw (vim)` 
To decode a cert:
```
openssl x509 [-in file] -text -noout
```

```
|   |   |
|---|---|
|/metrics|Prometheus metrics (kubelet itself)|
|/metrics/cadvisor|Container-level metrics|
|/metrics/resource|Resource plugin metrics|
|/metrics/probes|Liveness/readiness probe metrics|
|/stats/summary|Pod-level usage summary (used by metrics-server)|
|/logs|Logs for static pods|
|/configz|Kubelet configuration dump|
```

CNI directory:
```
/etc/cni/net.d
/opt/cni/bin
```

Use this to test ingress without setting /etc/hosts
```
curl --resolve demo.localdev.me:80:10.0.30.40 http://demo.localdev.me:80
```
```
-s silent
-w special format
-o save to file
-I get header only
-O save to file with name equal to resource
-k bypass tls verification
```

Check for any CM to know the controllerName

Remeber some commands and construct such as `while true; ... done` and `tail -f` and `sudo dpkg -i`

Use `helm get manifest` to get the manifest of a helm release\
`helm upgrade` -> must be very careful, need to always set --version, otherwise default to get latest version.

ResourceQuota: modify deployment still need delete old replicaset for resouce to be free

`kubectl get pod --show-labels` -> good for showing labels.

1000000000 is highest priority for user defined priority class.

Need to remove claimRef for pv to make it available.
```yaml
kubectl patch pv pv-for-rabbitmq -p '{"spec":{"claimRef": null}}'
```
Pod Cluster DNS:
`<pod-ip>.default.pod.cluster.local`

Use this to quickly nslookup a svc
```sh
kubectl run test-nslookup --image=busybox:1.28 --rm -it --restart=Never -- nslookup nginx-resolver-service-cka06-svcn
```
Most common CKA nginx-controller annotations:
|**Annotation**|**Description**|
|---|---|
|**ssl-redirect**|Redirect HTTP to HTTPS (default: "true" if TLS is configured)|
|**rewrite-target**|Rewrites the URI of the incoming request|
|**path-type** (not annotation, but Ingress spec)|Important to match exact (Exact) or prefix paths (Prefix)|
|**force-ssl-redirect**|Forces HTTPS redirect **even if TLS section is missing**|
|**whitelist-source-range**|IP whitelisting: allow only certain CIDRs to access|
|**default-backend**|Used in older versions to specify a catch-all backend (now usually handled via default ingressClass)|
|**enable-cors**, cors-allow-origin, etc.|For enabling CORS (if asked in web security scenarios)|
|**proxy-body-size**|Controls client upload limits (default is 1MB)|
|**auth-type, auth-secret**|For basic auth with username/password stored in a Secret|
|**configuration-snippet**|Allows custom NGINX directives to be added directly (use with caution)|

```
Use kubectl top nodes for metrics
```

Grep starting with `^ERROR`

```
curlimages/curl -> useful for debug with curl
```

**TROUBLESHOOTING**:

Can use `kubectl logs --previous` to check previous container logs if container keep restarting.

Debug cannot connect to kube-apiserver
```
- `/var/log/pods`
- `/var/log/containers`
- `crictl ps` + `crictl logs`
- `docker ps` + `docker logs` (in case when Docker is used)
- kubelet logs: `/var/log/syslog` or `journalctl`
- Use `journalctl -xeu kubelet` as the last resort to find control plane logs
```
RARE:
If kube api server fail intermittenly -> can be due to liveness probe: 

```
k get event -n kube-system | grep apiserver -> use this to check
```


```
Use kubectl events instead of kubectl get events in k8s > 1.26
```

https://kubernetes.github.io/ingress-nginx/user-guide/nginx-configuration/annotations/

strategic marge path: view patch merge key using https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.33 

`k get componentstatuses` -> get current cluster compontent status
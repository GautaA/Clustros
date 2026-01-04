# Kubernetes cluster debug & overview tool

This small Python tool helps inspect and debug a Kubernetes cluster. It can:

- Show a quick cluster overview (nodes, namespaces, pods, services, ingresses, deployments).
- Test DNS resolution using the cluster DNS.
- Test TCP connectivity to hosts/ports.
- Probe connectivity from inside the cluster by creating a short-lived debug pod and running `curl`/`ping`.
- Inspect TLS/SSL certificate presented by ingress hosts.

Requirements

Install dependencies (PowerShell):

```powershell
python -m pip install -r k8s_tool/requirements.txt
```

Usage examples

```powershell
# Full overview
python k8s_tool/k8s_overview.py --overview

# DNS test for a service name (e.g. kubernetes.default.svc.cluster.local)
python k8s_tool/k8s_overview.py --dns-test kubernetes.default.svc.cluster.local

# TCP connect test
python k8s_tool/k8s_overview.py --tcp-test example.com:443

# TLS cert inspect for host
python k8s_tool/k8s_overview.py --tls-check example.com:443

# Run in-cluster probe (create ephemeral pod) to curl an URL
python k8s_tool/k8s_overview.py --pod-probe http://kubernetes.default.svc.cluster.local
```

Notes

- The script tries to load `~/.kube/config` (local dev). If run from a pod inside the cluster it will use in-cluster config.
- Creating the debug pod requires permission to create and delete pods in the target namespace.

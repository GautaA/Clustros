# Kubernetes cluster debug & overview tool

This small Python tool helps inspect and debug a Kubernetes cluster. It can:

- Show a quick cluster overview (nodes, namespaces, pods, services, ingresses, deployments).
- **Display all nodes with current CPU and memory usage (color-coded, requires metrics-server):**
  - Shows CPU and memory usage as USED/MAX and percent, with green/yellow/red coloring for low/medium/high usage.
  - If metrics-server is not installed, a warning is shown and usage is omitted.
- Test DNS resolution using the cluster DNS.
- Test TCP connectivity to hosts/ports.
- Probe connectivity from inside the cluster by creating a short-lived debug pod and running `curl`/`ping`.
- Inspect TLS/SSL certificate presented by ingress hosts.

## Requirements
- Python 3
- Kubernetes Python client (`pip install kubernetes`)
- metrics-server installed in your cluster for resource usage metrics

## Usage

```sh
python3 k8s_overview.py --overview
```

This will show:
- Node names, roles, and ready conditions
- CPU and memory usage for each node (if metrics-server is available)
- Namespaces and pod counts
- Deployments, services, ingresses

Other flags:
- `--extra-checks` for additional cluster checks (API server version, kubelet versions, endpoints, events, PVCs, RBAC)
- `--dns-test HOST` to test DNS resolution
- `--tcp-test HOST:PORT` to test TCP connectivity
- `--tls-check HOST:PORT` to inspect TLS certificates
- `--pod-probe URL` to run a curl from inside the cluster

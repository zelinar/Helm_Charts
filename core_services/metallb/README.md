# Deploying MetalLB with a Custom IP Pool (Local Helm Chart, 2-Step Deployment)

This guide explains how to deploy [MetalLB](https://metallb.universe.tf/) from a local Helm chart in **two steps**:
1. Install MetalLB and its CRDs.
2. Deploy a custom `IPAddressPool` and `L2Advertisement` **after** the CRDs are ready.

## Why Two Steps?
MetalLB defines custom resource types:
- `IPAddressPool` (`metallb.io/v1beta1`)
- `L2Advertisement` (`metallb.io/v1beta1`)

If you try to install these resources **before** the CRDs exist, you will get errors like:
"no matches for kind "IPAddressPool" in version "metallb.io/v1beta1" ensure CRDs are installed first"

To avoid this, we separate the CRD installation from the custom resource creation.

---

## Prerequisites
- Kubernetes cluster
- `kubectl` configured to access your cluster
- [Helm](https://helm.sh/) installed
- Local MetalLB Helm chart available

---

## Step 1: Install MetalLB (Base Components)

From your local chart folder:

helm upgrade --install metallb . -f ./values.yaml \
  --namespace metallb \
  --create-namespace

Wait until MetalLB pods are running:

kubectl get pods -n metallb
Expected output (pod names may vary):

NAME                                  READY   STATUS    RESTARTS   AGE
metallb-controller-6b8f9d7b9f-abcde   1/1     Running   0          30s
metallb-speaker-xyz12                 1/1     Running   0          30s


deploy custom config:
helm upgrade --install metallb-ip-pool ./custom-ip-pool \
  --namespace metallb \
  -f ./values.yaml

Verify Deployment

kubectl get ipaddresspool -n metallb

NAME           AUTO ASSIGN   AVOID BUGGY IPS   ADDRESSES
custom-pool    true          false             ["100.100.100.10-100.100.100.20"]
bash

kubectl get l2advertisement -n metallb

NAME   IPADDRESSPOOLS
l2     ["custom-pool"]


Notes
Do not merge the IP pool resources into the first Helm install — the CRDs won’t exist yet.

Ensure the loadBalancerIP values you assign to services are within the configured IP pool range.

You can use hooks with post-install to automate the second step, but a two-step install is simpler and avoids webhook timing issues.


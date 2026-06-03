
```md
# Helm Charts Repository

This repository contains a collection of Helm charts for deploying and managing various applications and services in a Kubernetes cluster. It is structured to support a homelab environment with tools for observability, networking, storage, and more.

## Repository Structure

The repository is organized into the following directories:

- **argocd/**: Helm chart for deploying and managing ArgoCD.
- **core_services/**: Contains Helm charts for core services such as:
  - `cert-manager`: Certificate management.
  - `cnpg-operator`: PostgreSQL operator.
  - `homelab-tls`: Local CA for TLS certificates.
  - `longhorn`: Persistent storage solution.
  - `metallb`: Load balancer for bare-metal Kubernetes clusters.
  - `traefik`: Ingress controller.
- **ingress-nginx/**: Helm chart for deploying NGINX ingress controller.
- **k8s_dashboard/**: Helm chart for Kubernetes dashboard.
- **netbox/**: Helm chart for NetBox, an infrastructure resource modeling tool.
- **observability/**: Charts for monitoring and logging, including Prometheus and Grafana.
- **portainer/**: Helm chart for Portainer, a container management platform.
- **snipeit/**: Helm chart for Snipe-IT, an IT asset management system.
- **vault/**: Helm chart for HashiCorp Vault.
- **weblate/**: Helm chart for Weblate, a web-based translation tool.

## Prerequisites

- Kubernetes cluster
- Helm CLI installed
- `kubectl` configured to access your cluster

## Usage

### Adding the Repository

To add this repository to your Helm client:

```bash
helm repo add homelab-charts https://github.com/zelinar/Helm_Charts
helm repo update
```

### Installing a Chart

To install a chart, use the following command:

```bash
helm install <release-name> homelab-charts/<chart-name> -f 

values.yaml


```

Replace `<release-name>` with your desired release name and `<chart-name>` with the name of the chart you want to deploy.

### Example: Deploying ArgoCD

```bash
helm install argocd homelab-charts/argocd -f 

values.yaml


```

### Customizing Values

Each chart includes a `values.yaml` file that can be customized to suit your environment. Refer to the `values.yaml` file in each chart directory for available configuration options.

## Contributing

Contributions are welcome! Please follow these steps:

1. Fork the repository.
2. Create a new branch for your changes.
3. Submit a pull request with a detailed description of your changes.

## License

This repository is licensed under the Apache License 2.0. See the [LICENSE](LICENSE) file for details.

## References

- [Helm Documentation](https://helm.sh/docs/)
- [Kubernetes Documentation](https://kubernetes.io/docs/)

## License

This project is licensed under the GNU General Public License v3.0. See the [LICENSE](LICENSE) file for details.

## Author

- **GitHub**: [zelinar](https://github.com/zelinar)
```


# DevOpsHelmChartShopware

This project is part of the **DevOps** learning path of the Shopware Academy.

It shows the reference project state after the practical lab **Creating and Deploying a Shopware Helm Chart**.

It demonstrates how to:

- Package a Shopware Kubernetes deployment as a Helm chart.
- Use `Chart.yaml`, `values.yaml`, templates, and helper templates together.
- Configure Shopware, MySQL, Valkey, Services, storage, and Ingress through Helm values.
- Render and validate a chart before installing it.
- Preview environment-specific values without changing a running release.

Tested for **Shopware 6.7**.

## Reference Project

This repository is an educational reference state for the Academy practical lab. It is meant for comparing your local result with a known working project state.

You do not need to run this project to use it as a reference. The most important files to compare are:

- `Chart.yaml`
- `values.yaml`
- `values-production.yaml`
- `templates/_helpers.tpl`
- `templates/configmap.yaml`
- `templates/secret.yaml`
- `templates/pvc-mysql.yaml`
- `templates/mysql-deployment.yaml`
- `templates/redis-deployment.yaml`
- `templates/shopware-deployment.yaml`
- `templates/shopware-service.yaml`
- `templates/ingress.yaml`

These files show the expected Helm chart structure, values model, template rendering, labels, selectors, and local training configuration at the end of the lab.

It is not a production template. The bundled MySQL and Valkey resources, credentials, service names, storage setup, and runtime settings are intentionally simple for local learning.

## Optional: Render the Chart Locally

If you want to inspect the rendered Kubernetes manifests without creating resources in the cluster, run:

```bash
helm lint .
helm template my-shopware .
```

You can also preview the production values file:

```bash
helm template my-shopware . -f values-production.yaml
```

These commands only render output locally. They do not create a Helm release and they do not change a running cluster.

## Optional: Install the Chart Locally

If you want to run this reference project locally, you need a local Kubernetes cluster, an NGINX Ingress controller, Helm 3, `kubectl`, and the local image `shopware-devops-lp:local` from the practical labs.

Install the chart:

```bash
helm install my-shopware . \
  -n shopware-helm \
  --create-namespace \
  --timeout 5m
```

Check the resources:

```bash
kubectl get all -n shopware-helm
kubectl get ingress -n shopware-helm
```

When MySQL is ready, initialize Shopware from the running Shopware Pod as described in the practical lab.

Stop the setup:

```bash
helm uninstall my-shopware -n shopware-helm --ignore-not-found
kubectl delete namespace shopware-helm --ignore-not-found
```

## License

MIT License.

You may use this project in commercial and professional projects.
It is provided as an educational example and comes without a warranty and without support.

## Contributing

This project is part of the Shopware Academy curriculum.

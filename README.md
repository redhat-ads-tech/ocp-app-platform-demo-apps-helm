# OpenShift App Platform — Reusable Helm Charts

This repository contains two reusable Helm charts designed for the OpenShift Advanced App Platform Demo. They are consumed as dependencies by RHDH-scaffolded application manifests repos.

## Charts

| Chart | Description |
|---|---|
| **app-deployer** | Generic runtime deployer — renders Namespace, Deployment, Service, Route, HPA, NetworkPolicy, ServiceMonitor, Waypoint, and ServiceAccount resources for OpenShift. |
| **build-deployer** | Generic secured build pipeline deployer — renders Tekton Pipelines, Tasks, Triggers, ExternalSecrets, and webhook setup for CI with built-in security scanning (ACS, SBOM, TPA). Includes a production promotion pipeline that retags images via `skopeo copy` and opens a GitLab MR as an approval gate. |

## Helm Repository

Charts are published to GitHub Pages via [chart-releaser-action](https://github.com/helm/chart-releaser-action).

- **Repository index:** https://redhat-ads-tech.github.io/ocp-app-platform-demo-apps-helm/index.yaml
- **Releases:** https://github.com/redhat-ads-tech/ocp-app-platform-demo-apps-helm/releases

### Usage

Add the repository:

```bash
helm repo add app-platform https://redhat-ads-tech.github.io/ocp-app-platform-demo-apps-helm
helm repo update
```

Consume as a dependency in your `Chart.yaml`:

```yaml
dependencies:
  - name: app-deployer
    version: "~0.1"
    repository: "https://redhat-ads-tech.github.io/ocp-app-platform-demo-apps-helm"
    alias: app

  - name: build-deployer
    version: "~0.1"
    repository: "https://redhat-ads-tech.github.io/ocp-app-platform-demo-apps-helm"
    alias: build
```

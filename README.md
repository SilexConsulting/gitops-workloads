# GitOps workload catalogue

This repository is a workload catalogue intended to be
used in conjunction with https://github.com/SilexConsulting/gitops-control-plane

Please consult the README.md in that repository for more information.

## Resources (GIT-20)

Workload-owned raw manifests (e.g. an External Secrets `ExternalSecret` an app depends on) are
declared under `resources/` trees and applied by the **`workloads-resources`** ApplicationSet in
`bootstrap/resources.yaml`, which produces one Application per cluster: **`cluster-<name>-workloads-resources`**.
Gated per-cluster by the `enable_resources` label; three scopes, layered least→most specific:

- `environments/default/resources/` — applied to every cluster labelled `enable_resources=true`
- `environments/<env>/resources/` — per-environment
- `clusters/<cluster>/resources/` — per-cluster

Each dir has a root `kustomization.yaml` **listing** the manifests to apply — a manifest that
isn't listed (e.g. where the owning workload isn't enabled) is simply never rendered. Cluster-wide
resources (no workload owner) live in the **addons** repo, not here. Full design:
`gitops-control-plane/docs/git-20-resources-design.md`.

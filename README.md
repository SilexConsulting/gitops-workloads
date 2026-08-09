# GitOps workload catalogue

This repository is a workload catalogue intended to be
used in conjunction with https://github.com/SilexConsulting/gitops-control-plane

Please consult the README.md in that repository for more information.

## Resources (GIT-20)

Workload-scoped raw manifests (e.g. an External Secrets `ExternalSecret` an app depends on) are
declared under a `resources/` tree and applied by the `workload-resources` ApplicationSet in
`bootstrap/resources.yaml`:

- `environments/default/resources/` — applied to every cluster labelled `enable_resources=true`
- `environments/<env>/resources/` — per-environment
- `clusters/<cluster>/resources/` — per-cluster

Each `resources/` dir has a root `kustomization.yaml` listing the manifests to apply. Only listed
manifests are rendered, so a resource whose owning workload is disabled is simply left unlisted.
See `gitops-control-plane/docs/git-20-resources-design.md` for the full design.

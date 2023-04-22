# ArgoCD Vault Plugin

## Installation

- ConfigMap: cmp-plugin.yml
- ArgoCD: argocd.yml
  - Init Container
  - Sidecar Container

## Azure KeyVault

- KeyVault
- ServiceAccount with Role Assignment

## Usage

```yaml
kind: ConfigMap
apiVersion: v1
metadata:
  name: ocp4-test-configmap
data:
  # 'path': query as configured in ConfigMap
  # 'argo-cd-test': name of the KeyVault
  ocp-secret-key: <path:argo-cd-test#ocp-secret-value>
```

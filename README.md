# ArgoCD Vault Plugin

## OpenShift Operator Installation

- ConfigMap: cmp-plugin.yml
- ArgoCD: argocd.yml
  - Init Container
  - Sidecar Container

## Azure KeyVault Requirements

- KeyVault (e.g. with name 'argo-cd-test')
- AppRegistration (e.g. with name 'argo-cd-plugin')
- Role Assignment 'Key Vault Secrets User' to AppRegistration for KeyVault

## Usage in Resources

```yaml
kind: ConfigMap
apiVersion: v1
metadata:
  name: ocp4-test-configmap
data:
  # 'path': query as configured in ConfigMap (see cmp-plugin.yml)
  # 'argo-cd-test': name of the KeyVault (see above)
  ocp-secret-key: <path:argo-cd-test#ocp-secret-value>
```

## Configuration

See

- <https://argo-cd.readthedocs.io/en/stable/operator-manual/config-management-plugins/>
- <https://argocd-vault-plugin.readthedocs.io/en/stable/>
- <https://argocd-operator.readthedocs.io/en/latest/>

## Pitfalls

- Caching of Auth Result to KeyVault -> ArgoCD needs to be destroyed
- Usage of 'stringData' attribute in Secrets -> ArgoCD cannot sync 'non-base64' values
- When using a plugin, the 'directory' must not be set in Applications -> ArgoCD does not use the plugin

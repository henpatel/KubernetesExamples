
# Getting Started:

- Got the base with nginx basic templated helm chart and made it work by changing the values file with ingress enabled and class name to nginx.
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm install my-chart nginx

- To do the dry run and get the manifest that helm creates:
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm install my-chart nginx --dry-run

- To Delete the chart:
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm delete my-chart

- To see the template 
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm template my-chart nginx


# Builds manifest and shows the final output after the overlay.
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kustomize build overlays/ci

# Applies the configuration to kubernetes
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kubectl apply -k  overlays/dev       
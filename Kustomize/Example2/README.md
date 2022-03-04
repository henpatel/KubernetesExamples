
# Getting Started:
- Got the base with nginx basic templated helm chart and made it work by changing the values file with ingress enabled and class name to nginx.
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm install my-chart nginx
- To Delete the chart:
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> helm delete my-chart



# Builds manifest and shows the final output after the overlay.
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kustomize build overlays/ci

# Applies the configuration to kubernetes
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kubectl apply -k  overlays/dev       
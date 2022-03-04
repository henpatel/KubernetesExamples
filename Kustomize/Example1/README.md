

## Builds manifest based on the default base files
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build base
PS C:\Projects\KubernetesExamples\Kustomize\Example2\base> kustomize build

### You can build a base template file as below:
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kustomize build  base -o base-template.yaml



## Builds manifest and shows the final output after the overlay.
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kustomize build overlays/ci

## Applies the configuration to kubernetes
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kubectl apply -k  overlays/dev       
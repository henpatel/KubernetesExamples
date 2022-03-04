

## Builds manifest based on the default base files
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build base

## Builds manifest and shows the final output after the overlay.
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kustomize build overlays/ci

## Applies the configuration to kubernetes
PS C:\Projects\KubernetesExamples\Kustomize\Example1> kubectl apply -k  overlays/dev       
### You can build a base template file as below:
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build overlays/base -o base-template.yaml

For dev:
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build overlays/dev -o dev-template.yaml

For CI:
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build overlays/ci -o ci-template.yaml

For Prod:
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build overlays/ci -o ci-template.yaml


## Builds manifest and shows the final output after the overlay.
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kustomize build overlays/ci

## Applies the configuration to kubernetes
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl apply -k  overlays/dev 
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl apply -k  overlays/ci  
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl apply -k  overlays/prod


## To see all the resources that were created
kubectl get all --namespace=dev-meridian 

## Delete 
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl delete -k  overlays/dev
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl delete -k  overlays/ci
PS C:\Projects\KubernetesExamples\Kustomize\Example2> kubectl delete -k  overlays/prod
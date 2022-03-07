To use a customized values file for different enviornment:
PS C:\Projects\KubernetesExamples\Helm> helm template ci-chart Example1 --values example1/values.ci.yaml

or 

PS C:\Projects\KubernetesExamples\Helm\Example1> helm install  ci-chart ./ --values values.ci.yaml --namespace=ci-meridian --create-namespace


PS C:\Projects\KubernetesExamples\Helm\Example1> helm install  prod-chart ./ --values values.prod.yaml --namespace=prod-meridian --create-namespace




Cleanup:
PS C:\Projects\KubernetesExamples\Helm\Example1> helm delete dev-chart --namespace=dev-meridian
PS C:\Projects\KubernetesExamples\Helm\Example1> helm delete prod-chart --namespace=prod-meridian
PS C:\Projects\KubernetesExamples\Helm\Example1> helm delete ci-chart --namespace=ci-meridian 
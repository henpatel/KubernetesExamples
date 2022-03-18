##Installing Kong with Helm

NOTE: by default this installs kong in dbless mode.


```
> kubectl create namespace kong

> helm repo add kong https://charts.konghq.com
> helm repo update

## Switch to kong namespace and install kong
## Kong Gateway (OSS)
> helm install kong -n kong kong/kong --set ingressController.installCRDs=false

```
NAME: kong
LAST DEPLOYED: Thu Mar 17 14:39:39 2022
NAMESPACE: kong
STATUS: deployed
REVISION: 1
NOTES:
To connect to Kong, please execute the following commands:

HOST=$(kubectl get svc --namespace kong kong-kong-proxy -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
PORT=$(kubectl get svc --namespace kong kong-kong-proxy -o jsonpath='{.spec.ports[0].port}')        
export PROXY_IP=${HOST}:${PORT}
curl $PROXY_IP

Once installed, please follow along the getting started guide to start using
Kong: https://docs.konghq.com/kubernetes-ingress-controller/latest/guides/getting-started/


Port Forwarding for Kong Proxy:

```
> kubectl -n kong port-forward --address localhost,0.0.0.0 svc/kong-kong-proxy 8080:80
```

To look at the kong gateway:
```
curl localhost:8080

```

##Enable admin portal by getting the default values config and overwriting it with our own overrides

```
PS C:\Projects\KubernetesExamples\Helm\Kong\Helm> helm show values kong/kong > values.default.yaml
```

Create a values.yaml file and bring in the admin section and enable it and then upgrade the chart.

```
PS C:\Projects\KubernetesExamples\Helm\Kong\Helm> helm upgrade kong -n kong kong/kong -f values.dbless.yaml
```
Once completed you will see below:
Release "kong" has been upgraded. Happy Helming!
NAME: kong
LAST DEPLOYED: Thu Mar 17 15:02:52 2022
NAMESPACE: kong
STATUS: deployed
REVISION: 2
NOTES:
To connect to Kong, please execute the following commands:

HOST=$(kubectl get svc --namespace kong kong-kong-proxy -o jsonpath='{.status.loadBalancer.ingress[0].ip}')
PORT=$(kubectl get svc --namespace kong kong-kong-proxy -o jsonpath='{.spec.ports[0].port}')        
export PROXY_IP=${HOST}:${PORT}
curl $PROXY_IP

Once installed, please follow along the getting started guide to start using
Kong: https://docs.konghq.com/kubernetes-ingress-controller/latest/guides/getting-started/

----

Added a sample API helm chart via nginx at 
C:\Projects\KubernetesExamples\Helm\Kong\Api1
To Note here in the ingress class we set as 'Kong' for the ingress for nginx.

```
PS C:\Projects\KubernetesExamples\Helm\Kong\Api1> helm install api1 Helm 

```

Once this is done, we can verify the api available via api gateway:
http://localhost:8080/ with host header
or hostname: http://api1.kongtest.com:8080/

```
PS C:\Projects\KubernetesExamples\Helm\Kong\Api1> curl --header "Host:api1.kongtest.com" http://localhost:8080

```

----

###Also - you can just setup an ingress for existing urls setup in different namespaces as an example  with Ingress
Add a host file entry: 127.0.0.1 services.meridian.com
```
PS C:\Projects\KubernetesExamples\Helm\Kong\Ingress> kubectl apply -f kong-ingress.yml

```


References:
https://konghq.com/kong-builders/
https://konghq.com/videos/installing-kong-to-kubernetes-using-helm-part-2-kongbuilders/
https://github.com/Kong/demo-scene/tree/main/quotes-service/kubernetes
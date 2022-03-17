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


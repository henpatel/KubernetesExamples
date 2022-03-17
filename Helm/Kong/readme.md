
# To Install with Helm:
https://docs.konghq.com/gateway/2.8.x/install-and-run/helm/

###Create namespace
Create the namespace for Kong Gateway with Kubernetes Ingress Controller. For example:

```

kubectl create namespace kong

```

### Without DB-less mode
https://docs.konghq.com/gateway/2.8.x/install-and-run/kubernetes/

Note that in DB-less mode on Kubernetes, config is stored in etcd, the Kubernetes native datastore. For more information see Kubernetes Deployment Options.
get
kubectl apply -f https://bit.ly/kong-ingress-dbless

#Now run the following command to get details on kong-proxy:
kubectl -n kong get service kong-proxy

#Since we are not able to get the external-ip, just use the port-forwarding to access kong

kubectl -n kong port-forward --address localhost,0.0.0.0 svc/kong-proxy 8080:80


#To Delete Everything
kubectl delete -f https://bit.ly/kong-ingress-dbless

References:

https://docs.konghq.com/gateway/2.8.x/install-and-run/kubernetes/

https://medium.com/iotops/deploying-kong-api-gateway-in-kubernetes-all-the-what-why-where-and-some-how-questions-a9f91c661923

https://www.padok.fr/en/blog/kong-apigateway-kubernetes
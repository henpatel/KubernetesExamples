# Installing Kong with Helm
### documentation is listed at: [https://docs.konghq.com/gateway/2.8.x/install-and-run/helm/](https://docs.konghq.com/gateway/2.8.x/install-and-run/helm/)

## To get started
### You must create a namespace kong, and add the kong repository to your local and update
```
# Create Namespace kong
kubectl create namespace kong 

# Add the Kong Charts Repository - You can check the list of repos with "helm repo list"
helm repo add kong https://charts.konghq.com

#Update Helm
helm repo update
```

# Switch to kong namespace in VSCode and install kong with default db-less mode
## Install with DB-Less Mode without values file and any overrides
```
helm install kong -n kong kong/kong --set ingressController.installCRDs=false
```

## Install using values files overrides
- Multiple values files are added for reference:
  1. values.default.yaml - this file has the default values file - should not be changed, this file is just for reference
  1. values.adminapi.yaml - using this file we are enabling admin api mode and default db-less mode
  1. values.manager.yaml - using this file we are enabling admin api and manager ui
  1. values.postgreslocal.yaml - using this file we are enabling postgreslocal and admin api
- Run in KubernetesExamples\Kong directory the commands to get started with values config

### Install with Enabling admin api using ingress, DB-Less Mode:
Run the command as below to install the admin api and no db.
- Add "admin.kongproxy.meridian.com" to the host file.
```
127.0.0.1 admin.kongproxy.meridian.com
```
- Install Kong with admin api enabled
```
helm install kong -n kong kong/kong -f .\helm\values.adminapi.yaml
```

### Install with Enabling admin api and manager ui using ingress, DB-Less Mode:
Run the command as below to install the admin api and manager ui portal and no db.
NOTE: Add the admin api url and manager ui url to the host file to access the manager portal
```
127.0.0.1 admin.kongproxy.meridian.com
127.0.0.1 manager.kongproxy.meridian.com
```

- Install Kong with admin api and manager ui enabled
```
helm install kong -n kong kong/kong -f .\helm\values.manager.yaml
```

### To Install with postgres and just admin api enabled:
This config has kong installation with default bitnami postgres turned on
```
helm install kong -n kong kong/kong -f .\helm\values.postgreslocal.yaml
```

# Other commands for reference:

## Accessing the Gateway:
### Port Forwarding for Kong Proxy:
```
kubectl -n kong port-forward --address localhost,0.0.0.0 svc/kong-kong-proxy 8080:80
```

### access kong gateway:
```
curl localhost:8080
```

### Upgrade with install
```
helm upgrade --install kong -n kong kong/kong -f .\helm\values.postgreslocal.yaml
```

### Add a sample API and see the routing work
Added a sample API helm chart via nginx at Api1
To Note here in the ingress class we set as 'Kong' for the ingress for nginx.
```
PS C:\Projects\KubernetesExamples\Kong\Api1> helm install api1 Helm 
```

Once this is done, we can verify the api available via api gateway:
http://localhost:8080/ with host header
or hostname: http://api1.kongtest.com:8080/

```
PS C:\Projects\KubernetesExamples\Kong\Api1> curl --header "Host:api1.kongtest.com" http://localhost:8080

```

-----

#This is temporary testing commands you can ignore them

###Also - you can just setup an ingress for existing urls setup in different namespaces as an example  with Ingress
Add a host file entry: 127.0.0.1 services.meridian.com
```
PS C:\Projects\KubernetesExamples\Helm\Kong\Ingress> kubectl apply -f services-ingress.yml

```

To see the services gateway working - 
port forward:
kubectl -n kong port-forward --address localhost,0.0.0.0 svc/kong-kong-proxy 8080:80

and then access:
http://services.meridian.com:8080/apis/tenants/healthcheck
http://services.meridian.com:8080/apis/domains/healthcheck



-------
### TO test out default with database, you can just run the below command
```
helm template kong kong/kong -n kong --set admin.enabled=true --set admin.http.enabled=true --set postgresql.enabled=true --set postgresql.postgresqlUsername=kong --set postgresql.postgresqlDatabase=kong --set env.database=postgres

```

-------

References:
https://konghq.com/kong-builders/
https://konghq.com/videos/installing-kong-to-kubernetes-using-helm-part-2-kongbuilders/
https://github.com/Kong/demo-scene/tree/main/quotes-service/kubernetes
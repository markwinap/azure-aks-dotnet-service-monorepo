## Create Services
```sh
dotnet new webapi -n ServiceA.Api

dotnet new webapi -n ServiceB.Api
```

## Verify Subscriptions
```sh
az provider show -n Microsoft.OperationsManagement -o table
az provider show -n Microsoft.OperationalInsights -o table
```
## Register subscriptions
```sh
az provider register --namespace Microsoft.OperationsManagement
az provider register --namespace Microsoft.OperationalInsights
```
## Create resource group
```sh
az group create --name aksResourceGroup --location eastus
```

## Create AKS cluster
```sh
az aks create --resource-group aksResourceGroup --name myAKSCluster --node-count 1 --enable-addons monitoring --generate-ssh-keys
```
Install kubectl 
az aks install-cli

Configure kubectl to connect to your Kubernetes
az aks get-credentials --resource-group aksResourceGroup --name myAKSCluster

kubectl get nodes


## Deploy AKS App
kubectl apply -f azure-vote.yaml

## Test AKS App
kubectl get service azure-vote-front --watch

## Delete Cluster
az group delete --name myResourceGroup --yes --no-wait


docker build -t service_b_api:1.0 .

docker run service_b_api:1.0 -p 8080:80


docker run --name service_b_api --rm -it -p 8000:80/tcp service_b_api:latest


https://localhost:7193/swagger/index.html




dotnet build
dotnet run

https://localhost:7193/servicea


docker build -t service_a_api:latest .
docker run --name service_a_api --rm -it -p 8000:80 service_b_api:latest

http://localhost:8000/WeatherForecast


## Service B

### Run app locally
```sh
dotnet build
dotnet run
```

https://localhost:7045/serviceb

## Buiild Docker Image
```sh
docker build -t service_b_api:latest .
```
### Run Docker Image
```sh
docker run --name service_b_api --rm -it -p 8000:80 service_b_api:latest
```

### Test App
http://localhost:8000/serviceb



## Docker compose
```sh
docker-compose build
docker-compose up
```

http://localhost:8080/servicea
http://localhost:8081/serviceb


kubectl apply -f deployment.yaml

get pods
kubectl get pods
kubectl get services
ubectl get deployment

kubectl logs service-a-deployment-6cc44cc65c-mr572


kubectl delete deploy 
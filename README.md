# kubernetes-node-microservices
A kubernetes example running node.js microservices with application gateway

To run kubernetes in your computer, install minikube
start minikube
```
minikube start
```

Clone this repository, inside this repository folder, create all kubernetes services
```
kubctl create -f .
```

See the containers with 
```
kubctl get pods
```

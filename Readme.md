# K8S Task - Deploy 3 NGINX replicas

**Presented to:**    
_Mohammed Omar_    

**Presented by:**   
_Islam Khaled_    

13 June 2023

-----------------------------------------
## Create minikube cluster

![1](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/e5e88181-ae44-4535-8761-9e0fa775f58a)

-----------------------------------------
## Create nginx deployment with 3 replicas

- Code link for deployment yaml file: [nginx-depl.yaml](https://github.com/eslamkhaled560/Sprints-Tasks/blob/main/12-%20Kubenates/1-%20Deployments%20and%20Services/nginx-depl.yaml)

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 3
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

![2](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/826d0a9c-e280-4d76-b4fb-f11cf7899bdb)
![3](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/2c1eab2b-1ffc-4a70-beed-4e8ac7166d73)

-----------------------------------------
## Create service to point to this deployment , type cluster IP 

- Code link for service yaml file: [nginx-service.yaml](https://github.com/eslamkhaled560/Sprints-Tasks/blob/main/12-%20Kubenates/1-%20Deployments%20and%20Services/nginx-service.yaml)

```
apiVersion: v1
kind: Service
metadata:
  creationTimestamp: null
  name: nginx-deployment
spec:
  ports:
  - port: 80
    protocol: TCP
    targetPort: 80
  selector:
    app: nginx
  type: ClusterIP
status:
  loadBalancer: {}
```

![4](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/9eae97b2-bbd9-4514-a3b5-e453b1702923)

-----------------------------------------
##  Create debug pod to test the service

- Before installing curl

![5](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/a74f56a3-9c9e-4e8e-8b7d-f2631eab183e)

- After installing curl

![6](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/7acf556d-9afe-4979-891d-3cf8407b90c1)

-----------------------------------------

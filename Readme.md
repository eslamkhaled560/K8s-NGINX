# Description

Establishing a Local Kubernetes Environment and Deploying Replicas of Nginx Images for Internal Access via Cluster IP Service

-----------------------------------------
# Steps

- Clone repository and move to it
```
git clone https://github.com/eslamkhaled560/K8s-NGINX.git
cd K8s-NGINX
```

## Install Dependencies

- Create minikube cluster locally

```
curl -LO https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64
sudo install minikube-linux-amd64 /usr/local/bin/minikube
```

- Start minikube
```
minikube start
```

- Install kubectl
```
sudo apt-get update
sudo apt-get install -y ca-certificates curl
sudo apt-get install -y apt-transport-https       # for Debian based OS
echo "deb [signed-by=/etc/apt/keyrings/kubernetes-archive-keyring.gpg] https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee /etc/apt/sources.list.d/kubernetes.list
sudo apt-get update
sudo apt-get install -y kubectl
```

## Deploy Application

- Move to the application directory
```
cd K8s-NGINX
```

- Deploy application with the service
```
kubectl apply -f nginx-depl.yaml
kubectl apply -f nginx-service.yaml
```

- Get service ip, nginx-deployment Cluster-IP
```
kubectl get svc
```
You will find it inder: nginx-deployment Cluster-IP

- Check deplyment connection with a debug pod that will be destroys automatically after closing it.
```
kubectl run -it debug-pod --restart=Never --image=ubuntu -- bin bash
    ## inside debug-pod
    curl <nginx-deployment Cluster-IP>        # install curl if needed
```

- Output should look like this

![6](https://github.com/eslamkhaled560/Sprints-Tasks/assets/54172897/7acf556d-9afe-4979-891d-3cf8407b90c1)

-----------------------------------------

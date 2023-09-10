# Plotly Python app in K8s cluster
## Prerequisites
In order to be able to execute this project successfully we need to have this tools installed:

- Terraform
- Kubernetes
- minikube
- kubectl
- docker

## Steps to run the application
There is a docker image that was previously uploaded to the Docker hub repository, the name of the image is antoniofb3/python-app

To build the kubernetes cluster in minikube we need to run main.tf terraform file, go to plotly-homework root path and run

- terraform init
- terraform plan
- terraform apply

Once cluster is built, we can start the minikube
- minikube start

To verify that the cluster is up and running
- kubectl get nodes

To apply a deployment for the application
- kubectl apply -f python-app-deployment.yaml

We can scale the deployment up or down according to our needs, in this case we are scaling up to 5 replicas
- kubectl scale deployment python-app-deployment --replicas=5

I created a service to expose the Python app to the outside world, in this case I am using NodePort for this
- kubectl create -f python-app-service.yaml

I can display information about the Service I just created
- kubectl describe services python-app-service

I can list the pods that are running the application, in this case there are 5 pods
- kubectl get pods --selector="app=python-app" --output=wide

If we want to enable to the service from the outside world we can run the following command
- kubectl proxy

And finally go the URL provided in the output of the previous command to see the result
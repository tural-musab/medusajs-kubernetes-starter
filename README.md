# Medusa in Kubernetes

This project is a Kubernetes starter kit for deploying MedusaJS e-commerce applications. Forked and customized by tural-musab.

## Prerequisites

- Kubernetes cluster (preferably Minikube for development purposes)
- Node v22
- Yarn v4.7.0 (You should be able to enable it through corepack)

## Building the image

You should build the image before proceeding with further steps.

```bash
cd my-medusa-store
yarn build
docker build -t medusa-store:latest .
```

## Deploying your resources to K8s cluster

You should create a namespace to isolate your resources for easy clean-up and load the image

```bash
minikube image load medusa-store:latest
kubectl create namespace medusa
cd kubernetes
kubectl apply -f . -n medusa
```

## Accessing the Medusa instance

Once you have pushed all your resources to the cluster, you can use Minikube to create a tunnel to the load balancer. It is recommended to use [ngrok](https://ngrok.com) to use HTTPS for accessing the admin dashboard.

```bash
minikube tunnel 127.0.0.1
# In a seperate terminal you can run the following command
ngrok http 80

```

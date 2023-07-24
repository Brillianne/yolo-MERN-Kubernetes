## Choice of Kubernetes Objects for Deployments
A Deployment provides declarative updates for Pods

I created Deployments for both the backend and client containers. This is because Deployments are suitable for stateless apps where where each pod is independent, and it doesn't matter which pod handles a specific request.Deployments ensure that the desired number of replicas (pods) are running at all times, and they help manage rolling updates and rollbacks efficiently.

I created a StatefulSet for mongo container together with a persistent volume.StatefulSets are designed for stateful applications that require stable, unique network identities and persistent storage for each pod.StatefulSets provide guarantees about the ordering and uniqueness of pods

## Method used to expose your pods to internet traffic.

To expose your pods to internet traffic in Kubernetes, I used services to expose the pods with method below for my client container

NodePort:

NodePort is a simple way to expose your pods to the internet. It opens a specific port on all the nodes in the cluster and forwards traffic to the corresponding pods

## Use-of or there-lack-of of persistent storage.

 Persistent storage allows data to be preserved even if a pod is terminated, rescheduled to a different node, or scaled up or down.Persistent Volumes (PVs) and Persistent Volume Claims (PVCs) are used to provide and request persistent storage for StatefulSets. PVs are the actual storage resources, while PVCs are requests for that storage made by pods 

## Git workflow used to achieve the task.

## Step 1

Build the client and backend images i.e. backend and client images and push them to dockerhub.

##  Step 2

Create deployment files for both the backend and client container images

## Step 3

Create services for both the backend and client container images

## Step 4
Create a create the Deployment and service files and also add secrets for mongo username, password and MONGO_URI.

## Step 5
Deploy the file using below command

## kubectl apply -f <filename>

in below order

secrets file
Deployment files
Service files
## Step 6
So that you can be able to access the service you will need to port forward for both the the backend and client services

For backend use below command

kubectl port-forward service/yolo-backend-service 5050:5050 For client to be able to access the client service in your browser

kubectl port-forward service/client-service 3000:3000

Challenge dependency issues for client app, Yolo app was build with a previos version of react that may not support env variables 

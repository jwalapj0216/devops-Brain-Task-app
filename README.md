# Devops Braintask project
Create an EC2 instance with admin or required accesss 

The main requirement for the project is :

- EC2 instance with required access also can use role (adminaccess)
- docker
- aws cli
- kubectl
- eksctl

## Pipeline 

Source --> Build ---> deploy 

- source will get trigered when some commit happens in github (developer commit code). It will get all the code
- Build will create a docker image and upload in ECR, code build is used to run the docker command and upload and create the environement for running app
- Deploy will run deply the application in kubernetes cluster 

## Creating an ECR Repository for the project

we can create ECR repository jwala/brain-app either using GUI or by below clicommand 

```sh
aws ecr create-repository \
--repository-name brain-app-repo \
--region ${AWS_REGION}
```

## Create EKS cluster

```sh
eksctl create cluster \
--name brain-project-cluster1 \
--region us-east-1 \
--nodegroup-name brain-nodes1 \
--node-type t3.micro \
--nodes 2 \
--nodes-min 2 \
--nodes-max 3 \
--managed
```
setup
=====
aws eks update-kubeconfig --region us-east-1 --name brain-project-cluster1

confirm cluser
==============
eksctl get cluster --region us-east-1
aws eks describe-cluster --name brain-project-cluster1 --region us-east-1
aws eks list-clusters --region us-east-1


### For checking if the node created fine use below commands 

This code will provide space there will be memory issue for t3.micro  if you proceed without this scale up some time you will meet with this space issue error 

"

  Warning  FailedScheduling  20m                  default-scheduler  0/2 nodes are available: 1 Insufficient memory, 2 Too many pods. no new claims to deallocate, preemption: 0/2 nodes are available: 2 No preemption victims found for incoming pod.
  Warning  FailedScheduling  9m58s (x2 over 14m)  default-scheduler  0/2 nodes are available: 1 Insufficient memory, 2 Too many pods. no new claims to deallocate, preemption: 0/2 nodes are available: 2 No preemption victims found for incoming pod.

"
```sh
eksctl scale nodegroup \
--cluster brain-project-cluster1 \
--name brain-nodes1 \
--nodes 3 \
--region us-east-1
```
Create namespace brain 
kubectl create namespace brain

### To see the hosted site and get url 
kubectl get pods -n brain
kubectl get svc -n brain


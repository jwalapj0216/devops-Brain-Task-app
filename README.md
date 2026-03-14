# Devops Braintask project
Create an EC2 instance with admin or required accesss 

The main requirement for the project is :

- EC2 instance with required access also can use role (adminaccess)
- docker
- aws cli
- kubectl
- eksctl

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
for checking if the node created fine 
use below commands 

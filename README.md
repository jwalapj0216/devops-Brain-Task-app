# Devops Braintask project

The main requirement for the project is :

- EC2 instance with required access also can use role (adminaccess)
- docker
- aws cli
- kubectl
- eksctl

## Creating an ECR Repository for the project

```sh
aws ecr create-repository \
--repository-name brain-app-repo \
--region ${AWS_REGION}
```

## Create EKS cluster

```sh
eksctl create cluster \
--name brain-cluster \
--region ap-south-1 \
--node-type t3.medium \
--nodes 2
```

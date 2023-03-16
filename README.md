# Terraform AWS VPC and EKS Cluster

This Terraform codebase creates an AWS VPC and deploys an EKS cluster within the VPC. The EKS cluster is deployed across multiple Availability Zones (AZs) within the specified AWS region, and worker nodes are automatically provisioned in an Auto Scaling Group (ASG) using the Amazon Elastic Container Service for Kubernetes (EKS) optimized Amazon Machine Image (AMI).

## High Level Architecture

The following is the high level architecture diagram of the resources spun by terraform and teh connectivity between then in AWS.

![image](https://user-images.githubusercontent.com/126039883/225699887-9fab91ee-4afe-4803-b504-a80e31540cd0.png)


## Prerequisites

Before you can deploy this infrastructure using Terraform, you will need to have the following:

- An AWS account and IAM user with sufficient permissions to create VPCs, EKS clusters, and associated resources.
- The AWS CLI installed and configured on your local machine.
- Terraform installed on your local machine.

## Usage

To use this Terraform codebase to create an AWS VPC and deploy an EKS cluster:

1. Clone this repository to your local machine:
> git clone https://github.com/sravankumar234/AWS-Terraform.git

2. Navigate to the repository directory:
> cd aws-terraform/

3. Initialize the Terraform project by running:
> terraform init

4. Set the required variables by creating a **terraform.tfvars** file and populating it with the appropriate values:
```
access_key = ""
secret_key = ""
name = ""  #name of vpc
region = "us-east-1"
cidr_block = "10.0.0.0/16"  # CIDR block of vpc
public_subnet_cidr_blocks = ["10.0.1.0/24","10.0.2.0/24"]
private_subnet_cidr_blocks = ["10.0.3.0/24","10.0.4.0/24"]
cluster_private_access = true
cluster_public_access = true
availability_zones = ["us-east-1a", "us-east-1b"]

```
5. Provision the AWS infrastructure by running:
> terraform apply

6. Configure kubectl to use the newly created EKS cluster:
> aws eks update-kubeconfig --name my-eks-cluster --region us-east-1


## Cleaning up

To remove the AWS infrastructure that was created by this Terraform codebase, run:

> terraform destroy

This will destroy all resources created by Terraform, including the VPC, subnets, internet gateway, route tables, security groups, and EKS cluster.

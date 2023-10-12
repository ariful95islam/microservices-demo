# My EKS Application Infrastructure

This repository contains Terraform configurations and Kubernetes deployments for setting up an EKS-based application. This is the helmfile version. More details on this method can be found here: [Deployment with Helmfile](https://exciting-amusement-090.notion.site/K8s-Microservices-0ef8f69d41f84ded9ac1229c60aee801?pvs=4)

## Directory Structure

- `vpc.tf`: Terraform configuration for AWS VPC setup.
- `eks-cluster.tf`: Terraform configuration for AWS EKS cluster setup.
- `helmcharts`: Kubernetes deployment configuration for the application microservices via helmfile.

## Prerequisites

- Terraform installed
- AWS CLI configured with necessary permissions
- `kubectl` installed for Kubernetes configurations
- `aws-iam-authenticator` installed
- `helmfile` installed

## Setup Instructions

1. **Set Up AWS VPC**:
   ```bash
   terraform init
   terraform apply -target module.myapp-vpc
   ```

2. **Deploy EKS Cluster**:
   ```bash
   terraform apply -target module.eks
   ```

3. **Configure kubectl for EKS**:
   ```bash
   aws eks update-kubeconfig --region <REGION> --name <CLUSTER_NAME>
   ```

4. **Deploy Kubernetes Configurations**:
   ```bash
   cd helmcharts
   helmfile lint
   helmfile sync
   ```

## Important Notes

- The VPC is configured with both private and public subnets.
- The EKS cluster is set up in the defined VPC and is tagged for development purposes.

## Cleanup

To destroy the created infrastructure:
```bash
helmfile destroy
terraform destroy
```

## Contributions

Feel free to raise issues or pull requests if you wish to contribute to the infrastructure or application configurations.

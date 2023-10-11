# My EKS Application Infrastructure

This repository contains Terraform configurations and Kubernetes deployments for setting up an EKS-based application. This is the best practices version. More details on the best practices can be found here: [K8s Config Best Practices](https://exciting-amusement-090.notion.site/K8s-Best-Practices-a8d0410b3d17467f9164b6a19df7ad95?pvs=4)

## Directory Structure

- `vpc.tf`: Terraform configuration for AWS VPC setup.
- `eks-cluster.tf`: Terraform configuration for AWS EKS cluster setup.
- `k8s-config.yaml`: Kubernetes deployment configuration for the application microservices.

## Prerequisites

- Terraform installed
- AWS CLI configured with necessary permissions
- `kubectl` installed for Kubernetes configurations
- `aws-iam-authenticator` installed

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
   kubectl apply -f k8s-config.yaml
   ```

## Important Notes

- The VPC is configured with both private and public subnets.
- The EKS cluster is set up in the defined VPC and is tagged for development purposes.
- The `k8s-config.yaml` deploys an email service to the EKS cluster.

## Cleanup

To destroy the created infrastructure:
```bash
kubectl delete -f k8s-config.yaml
terraform destroy
```

## Contributions

Feel free to raise issues or pull requests if you wish to contribute to the infrastructure or application configurations.

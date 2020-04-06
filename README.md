# K8s Metrics Server Terraform Module

## Introduction

Terraform modules for deploying [Kubernetes Metric Server](https://github.com/kubernetes-sigs/metrics-server).

Supported Kubernetes Dashboard Version: `v0.3.6`

**Terraform version**: `0.12.23`

## Example

```hcl-terraform

# Connecting to AWS EKS

data "aws_eks_cluster" "cluster" {
  name = var.cluster_id
}

data "aws_eks_cluster_auth" "cluster" {
  name = var.cluster_id
}
   
provider "kubernetes" {
  host                   = data.aws_eks_cluster.cluster.endpoint
  cluster_ca_certificate = base64decode(data.aws_eks_cluster.cluster.certificate_authority.0.data)
  token                  = data.aws_eks_cluster_auth.cluster.token
  load_config_file       = false
}

# Installing metrics-server

module "kubernetes_metrics_server" {
  source = "git@github.com/k8s-zoo/k8s-metrics-server-terraform-module.git//terraform"
}
```
 
**Variables**: For info on variables, check [file](terraform/variables.tf)
    
## Overview

- **Maintainer**: mishalshah92@gmail.com

# DEPI HelloApp Infrastructure v2

[![Terraform](https://img.shields.io/badge/IaC-Terraform-844FBA?logo=terraform)](https://www.terraform.io/)
[![AWS](https://img.shields.io/badge/Cloud-AWS-232F3E?logo=amazonaws)](https://aws.amazon.com/)
[![Kubernetes](https://img.shields.io/badge/Platform-EKS-326CE5?logo=kubernetes)](https://aws.amazon.com/eks/)
[![Jenkins](https://img.shields.io/badge/CI%2FCD-Jenkins-D24939?logo=jenkins)](https://www.jenkins.io/)
[![Terraform CI](https://github.com/fadyy2k/depi-helloapp-infra-v2/actions/workflows/terraform-ci.yml/badge.svg)](https://github.com/fadyy2k/depi-helloapp-infra-v2/actions/workflows/terraform-ci.yml)

Terraform-based AWS infrastructure lab for the DEPI DevOps track. The repository focuses on modular infrastructure, EKS, networking, IAM, security groups, remote state, and Jenkins-driven Terraform workflows.

## Architecture

```text
Jenkins
  │
  ├── terraform init / plan
  │
  ▼
AWS
  ├── VPC
  ├── Public + private subnets
  ├── IAM
  ├── Security groups
  └── EKS + worker nodes
```

## Repository Layout

- `main.tf` — root infrastructure composition
- `modules/` — reusable VPC, EKS, IAM and security-group modules
- `backend.tf` — remote-state configuration
- `providers.tf` — AWS and Kubernetes providers
- `variables.tf` / `outputs.tf` — module inputs and outputs
- `Jenkinsfile` — Terraform pipeline stages
- `terraform.tfvars.example` — sanitized example inputs

## Security

- Real account IDs and administrator CIDRs are not published.
- Do not commit `.tfvars`, credentials, state files, kubeconfig, or cloud access keys.
- The example IAM mapping is deliberately non-admin; grant production access through least-privilege roles and an approved access process.
- Restrict SSH/admin ingress to trusted CIDRs or, preferably, private management paths.

## Quick Start

```bash
cp terraform.tfvars.example terraform.tfvars
terraform init
terraform validate
terraform plan
```

Review the plan before any apply. This repository is a lab/reference implementation, not a drop-in production environment.

## Engineering Notes

The useful part of this project is the separation of network, identity, security-group and EKS concerns into reusable modules. Production evolution would add policy-as-code, CI security scanning, protected remote state, short-lived cloud credentials, and explicit approval gates.

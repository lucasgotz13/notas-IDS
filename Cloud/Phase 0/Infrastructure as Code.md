---
tags:
  - cloud
---
# What is it?
**Infrastructure as Code** (IaC) is a mainstream pattern for managing infrastructure with **configuration files** rather than GUI's or manual command line script sequences. It allows you to build, change, and manage your infrastructure in a safe, consistent, traceable and repeatable way by defining resource configurations that you can version (GitHub), reuse and share. IaC can be deployed in an **immutable way or changed in place** without redeploying 

The most commonly used tool for IaC is ***Terraform***.
# What is Terraform?
Terraform is a IaC tool that lets you define both **cloud** and **on-prem** resources in **human-readable configuration files**, that can be versioned, resued and shared. With these files, you can then use a consistent workflow to provision and manage all of your infrastructure throughout its lifecycle.
Terraform can manage both low-level and high-level components.

## How does Terraform work?
Terraform creates and manages resources through their APIs. Providers enable Terraform to work with virtually any platform or service with an accessible API.

The core Terraform workflow consists of three stages:
- **Write**: You define resources, which may be across multiple cloud providers and services.
- **Plan**: Terraform creates an execution plan describing the infrastructure it will create, update, or destroy based on the existing infrastructure and your configuration
- **Apply**: On approval, Terraform performs the necessary operations in the correct order, respecting any resource dependencies.
## Commands
-  `terraform init`: initializes a working directory containing Terraform configuration files. This is the first command you should run after writing a new Terraform configuration or cloning an existing configuration from version control. It is safe to run this command multiple times.
- `terraform apply`: executes the operations proposed in a Terraform plan.

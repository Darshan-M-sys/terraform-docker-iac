# DevOps Internship Task 3 - Infrastructure as Code with Terraform

## Objective

The objective of this task is to understand and implement **Infrastructure as Code (IaC)** using Terraform.

In this task, Terraform is used to provision and manage a Docker container automatically using code instead of manually creating the container.

---

## Tools Used

- Terraform v1.16.5
- Docker v29.2.1
- Ubuntu
- Git
- GitHub

---

## What is Infrastructure as Code?

Infrastructure as Code (IaC) is the practice of managing and provisioning infrastructure using configuration files and code instead of manually configuring it.

For example, instead of manually creating a Docker container, we can define the container in Terraform:

```hcl
resource "docker_container" "nginx" {
  name  = "terraform-nginx"
  image = docker_image.nginx.image_id
}
```

# Project Structure
terraform-docker-task/
│
├── main.tf
├── README.md
├── .gitignore
├── .terraform.lock.hcl
│
└── execution-logs/
    ├── terraform-init.png
    ├── terraform-plan.png
    ├── terraform-apply.png
    ├── terraform-state.png
    ├── docker-container.png
    └── terraform-destroy.png

### Terraform Configuration
terraform {
  required_providers {
    docker = {
      source  = "kreuzwerker/docker"
      version = "~> 3.0"
    }
  }
}

provider "docker" {}

resource "docker_image" "nginx" {
  name = "nginx:latest"
}

resource "docker_container" "nginx" {
  name  = "terraform-nginx"
  image = docker_image.nginx.image_id

  ports {
    internal = 80
    external = 8080
  }
}

# DevOps Internship Task 3: Infrastructure as Code with Terraform

## 📌 Project Overview

This project demonstrates **Infrastructure as Code (IaC)** using Terraform and Docker. Terraform is used to define, provision, and manage Docker resources through configuration files.

In this project, Terraform downloads the Nginx Docker image and creates a Docker container named `terraform-nginx`. The Nginx web server is accessible through port `8081` on the local machine.

## 🎯 Objective

- Understand Infrastructure as Code (IaC).
- Learn how Terraform manages infrastructure.
- Configure Terraform with the Docker provider.
- Create a Docker container using Terraform.
- Practice Terraform initialization, validation, planning, applying, state inspection, and destruction.
- Document the implementation with screenshots.

## 🛠️ Technologies Used

- **Terraform** — Infrastructure provisioning.
- **Docker** — Containerization platform.
- **Nginx** — Web server.
- **Visual Studio Code** — Code editor.
- **Git and GitHub** — Version control and project submission.

## 📂 Project Structure

```text
devops-task-03/
├── main.tf
├── README.md
├── .gitignore
└── screenshots/
    ├── terraform-init.png
    ├── terraform-validate.png
    ├── terraform-plan.png
    ├── terraform-apply.png
    ├── docker-ps.png
    ├── nginx-page.png
    ├── terraform-state.png
    └── terraform-destroy.png
```

*Note: Replace the example screenshot filenames with the names of your actual images.*

## ⚙️ Prerequisites

Install the following tools before running the project:

1. Terraform
2. Docker Desktop
3. Visual Studio Code
4. Git

Verify the installations:

```bash
terraform -version
docker --version
git --version
```

Ensure Docker Desktop is running before executing Terraform commands.

## 📝 Terraform Configuration

The `main.tf` file defines the Docker provider, Nginx image, and Docker container.

```hcl
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

resource "docker_container" "nginx_container" {
  name  = "terraform-nginx"
  image = docker_image.nginx.image_id

  ports {
    internal = 80
    external = 8081
  }
}
```

### Configuration Explanation

- **Terraform block:** Specifies the required Docker provider.
- **Docker provider:** Connects Terraform to Docker.
- **Docker image resource:** Downloads the `nginx:latest` image if needed.
- **Docker container resource:** Creates a container named `terraform-nginx`.
- **Internal port 80:** The port used by Nginx inside the container.
- **External port 8081:** Maps the local machine's port to container port 80.

## 🚀 Implementation Steps

### Step 1: Initialize Terraform

```bash
terraform init
```

Downloads the required provider plugins and initializes the working directory.

### Step 2: Validate the Configuration

```bash
terraform validate
```

Checks whether the Terraform configuration is valid.

### Step 3: Review the Execution Plan

```bash
terraform plan
```

Displays the infrastructure changes Terraform intends to make.

### Step 4: Create the Infrastructure

```bash
terraform apply
```

Review the proposed changes and type `yes` when prompted.

Terraform downloads the Nginx image if needed and creates the Docker container.

### Step 5: Verify the Docker Container

```bash
docker ps
```

Confirms whether the container is running.

### Step 6: Access the Nginx Web Server

Open the following address in your browser:

http://localhost:8081

The Nginx welcome page should appear while the container is running and the port is accessible.

### Step 7: Inspect Terraform State

```bash
terraform state list
```

Lists the resources currently recorded in Terraform state.

### Step 8: Destroy the Infrastructure

```bash
terraform destroy
```

Review the proposed deletions and type `yes` when prompted.

This removes the Terraform-managed container and image resource according to the resource lifecycle and dependencies.

## 📸 Screenshots

Store your actual screenshots in the `screenshots/` directory.

Recommended screenshots:

1. Terraform initialization.
2. Terraform validation.
3. Terraform plan.
4. Terraform apply completion.
5. Docker container running.
6. Nginx welcome page.
7. Terraform state list.
8. Terraform destroy completion.

### Screenshot Previews

Update the filenames below to match your actual screenshots.

#### Terraform Initialization
![Terraform Init](screenshots/terraform-init.png)

#### Terraform Validation
![Terraform Validate](screenshots/terraform-validate.png)

#### Terraform Plan
![Terraform Plan](screenshots/terraform-plan.png)

#### Terraform Apply
![Terraform Apply](screenshots/terraform-apply.png)

#### Docker Container
![Docker PS](screenshots/docker-ps.png)

#### Nginx Web Page
![Nginx Page](screenshots/nginx-page.png)

#### Terraform State
![Terraform State](screenshots/terraform-state.png)

#### Terraform Destroy
![Terraform Destroy](screenshots/terraform-destroy.png)

## 📚 Key Learning Outcomes

- Understood Infrastructure as Code and its benefits.
- Learned how Terraform providers interact with Docker.
- Created Docker resources using declarative configuration.
- Practiced Terraform initialization, validation, planning, applying, and destroying.
- Learned the purpose of Terraform state.
- Verified a containerized web server using Docker and a browser.

## 🧹 Cleanup

After verifying the application, run:

```bash
terraform destroy
```

Then check the running containers:

```bash
docker ps
```

The Nginx page will no longer be accessible after the container is removed.

## ✅ Conclusion

This project demonstrates how Terraform automates the provisioning and lifecycle management of a Docker-based Nginx web server. It provides practical experience with Infrastructure as Code, containerization, Terraform state, and infrastructure cleanup.

**Task:** DevOps Internship — Task 3  
**Project:** Infrastructure as Code with Terraform and Docker  
**Status:** Completed locally; ready for GitHub submission after verifying the project files and screenshots.

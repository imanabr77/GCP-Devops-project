# GCP-Devops-project

This project demonstrates how to deploy a simple Go application on Google Kubernetes Engine (GKE) using Terraform for infrastructure provisioning and Kubernetes manifests for application deployment. It also includes a CI/CD pipeline using GitHub Actions for automated builds and deployments.

![Alt text](<GCP Devops Project.jpg>)

## Table of Contents

1. [Project Overview](#project-overview)
2. [Project Structure](#project-structure)
3. [Prerequisites](#prerequisites)
4. [Setup Instructions](#setup-instructions)
5. [CI/CD Pipeline](#ci-cd-pipeline)
6. [Accessing the Application](#accessing-the-application)
7. [Cleaning Up](#cleaning-up)
8. [Contributing](#contributing)
10. [Acknowledgments](#acknowledgments)

## Project Overview

This project includes:

- A simple Go web application that serves a "Hello from GKE!" message.
- Terraform scripts to provision a GKE cluster and node pool.
- Kubernetes manifests to deploy the application on the GKE cluster.
- A GitHub Actions workflow for CI/CD to automate building, pushing, and deploying the application.

## Project Structure
````
.
├── go-app
│   ├── main.go                # Go application code
│   └── Dockerfile             # Dockerfile to containerize the Go app
├── k8s
│   ├── deployment.yaml        # Kubernetes deployment manifest
│   ├── service.yaml           # Kubernetes service manifest
│   └── namespace.yaml         # Kubernetes namespace manifest
├── terraform
│   ├── main.tf                # Terraform configuration for GKE
│   ├── variables.tf           # Terraform variables
│   └── outputs.tf             # Terraform outputs
└── .github
    └── workflows
        └── ci-cd.yaml        # GitHub Actions CI/CD workflow
````
## Prerequisites

Prerequisites
Before you begin, ensure you have the following:

Google Cloud Platform (GCP) Account:

Create a GCP project and enable the Kubernetes Engine API.

Google Cloud SDK:

Install the Google Cloud SDK.

Terraform:

Install Terraform.

## Setup Instructions

1. Clone the Repository

````
git clone https://github.com/your-username/your-repo.
git cd your-repo
````
2. Initialize and Apply Terraform
   Navigate to the terraform directory and initialize Terraform:
 ````
   cd terraform terraform init
````
   Apply the Terraform configuration to create the GKE cluster:
````  
   terraform apply -var="project_id=<YOUR_GCP_PROJECT_ID>"
````


3. Set Up GitHub Secrets
   Add the following secrets to your GitHub repository:
   ````
   - GCP_PROJECT_ID: Your GCP project ID.
   - GCP_SA_KEY: The content of your service account JSON key file.
   ````

4. Push to GitHub
   Commit and push the code to your GitHub repository:
   ````
    git add . git commit -m "Initial commit" 
    git push origin main
   ````

## CI/CD Pipeline

The CI/CD pipeline is defined in `.github/workflows/ci-cd.yaml`. It performs the following steps:
- Builds the Docker image for the Go application.
- Pushes the image to Google Container Registry (GCR).
- Updates the Kubernetes deployment manifest with the new image tag.
- Applies the Kubernetes manifests to deploy the application.

## Accessing the Application

After the CI/CD pipeline completes, get the external IP of the LoadBalancer service:
kubectl get svc go-app-service -n go-app

Visit `http://<EXTERNAL_IP>` in your browser to see the "Hello from GKE!" message.

## Cleaning Up

To avoid unnecessary charges, destroy the GKE cluster and associated resources:
cd terraform terraform destroy -var="project_id=<YOUR_GCP_PROJECT_ID>"


## Contributing
Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or submit a pull request.


## Acknowledgments

- Google Cloud for providing the GKE platform.
- Terraform for infrastructure as code.
- GitHub Actions for CI/CD automation.
- Enjoy deploying your Go application on GKE! 🚀



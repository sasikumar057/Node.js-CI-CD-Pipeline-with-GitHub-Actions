# Node.js-CI-CD-Pipeline-with-GitHub-Actions

This repository demonstrates a complete CI/CD pipeline for a Node.js application using **GitHub Actions**, **Docker**, and **Kubernetes**.

## Features
1. **Run Tests Automatically**: The pipeline runs tests on pull requests using **Jest**.
2. **Build and Push Docker Image**: The app is containerized using **Docker** and the image is pushed to **DockerHub**.
3. **Kubernetes Deployment**: The app is deployed to a **Kubernetes** cluster.
4. **Notifications**: Deployment success/failure notifications are sent via **Telegram**.

## Tools Used
- **GitHub Actions** for CI/CD automation.
- **Docker** for containerization.
- **Kubernetes** for deployment.
- **Telegram** for deployment notifications.

Before setting up the CI/CD pipeline, make sure the following tools are installed and set up on your local machine:

    Node.js (LTS version) and npm for managing dependencies.
    Docker to containerize the Node.js application.
    Kubernetes (minikube or cloud-based Kubernetes like GKE, EKS, or AKS).
    GitHub account to host the repository and create workflows.

Setup and Usage
Step 1: Clone the Repository

Clone this repository to your local machine:

git clone https://github.com/<your-username>/nodejs-ci-cd.git
cd nodejs-ci-cd

Step 2: Replace Your DockerHub Username

In the Dockerfile and the GitHub Actions workflow (.github/workflows/ci-cd-pipeline.yml), replace <YOUR_DOCKERHUB_USERNAME> with your actual DockerHub username.

# In Dockerfile
# Replace <YOUR_DOCKERHUB_USERNAME> with your username
docker build -t <YOUR_DOCKERHUB_USERNAME>/nodejs-app:latest .

Step 3: Add Required GitHub Secrets

For the CI/CD pipeline to work, you need to add the following secrets to your GitHub repository:

    DOCKER_USERNAME: Your DockerHub username.
    DOCKER_PASSWORD: Your DockerHub password or access token.
    KUBECONFIG_JSON: Your Kubernetes configuration (base64 encoded).
    TELEGRAM_CHAT_ID: Your Telegram chat ID (where you want the notifications).
    TELEGRAM_TOKEN: Your Telegram bot token (generated from BotFather).

To add secrets in GitHub:

    Go to your GitHub repository > Settings > Secrets > Actions.
    Click on New repository secret and add each of the above secrets.

Step 4: Push Changes to GitHub

Once your repository is set up, push your code and workflow to GitHub:

git add .
git commit -m "Set up CI/CD pipeline with Docker and Kubernetes"
git push origin main

Step 5: Trigger the Pipeline

Once you push changes to the main branch or create a pull request, GitHub Actions will automatically trigger the pipeline to:

    Run tests using npm test.
    Build the Docker image and push it to DockerHub.
    Deploy the application to your Kubernetes cluster.
    Notify you via Telegram about the deployment status.

How It Works
Triggering the Pipeline

The pipeline is triggered by:

    Pushes to the main branch.
    Pull requests targeting the main branch.

Pipeline Steps

    Test: The pipeline first runs npm test to ensure the application works correctly.
    Build & Push: The Docker image is built using the Dockerfile, tagged with your DockerHub username, and pushed to DockerHub.
    Deploy to Kubernetes: The app is deployed to the Kubernetes cluster using the kubectl apply command with the deployment.yaml and service.yaml files.
    Notifications: If the deployment is successful, a message is sent to your Telegram chat using the Telegram bot token.

Troubleshooting

    If the Docker image is not pushing to DockerHub, ensure that your DOCKER_USERNAME and DOCKER_PASSWORD GitHub secrets are correctly set.
    If the Kubernetes deployment fails, verify that your KUBECONFIG_JSON secret contains the correct Kubernetes configuration.
    If Telegram notifications are not sent, check that TELEGRAM_TOKEN and TELEGRAM_CHAT_ID are correct and that the Telegram bot is configured correctly.

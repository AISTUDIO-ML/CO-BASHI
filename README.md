# CO-BASHI

Welcome to **Co-Bashi**, a SaaS platform designed to empower Linux administrators and DevOps teams with secure, scalable shell script automation.

---

## 🚀 Introduction

Co-Bashi helps streamline Linux operations by providing a centralized platform for managing, executing, and monitoring shell scripts across distributed systems. It integrates modern DevOps practices with traditional scripting workflows.

---

## 🧠 Tech Stack

- **Backend**: FastAPI (Python)
- **Frontend**: React + TypeScript
- **Execution Engine**: Docker-based sandbox or SSH runner
- **CI/CD**: GitHub Actions
- **License**: MIT

---

## ✨ Key Features

- Script repository with version control
- Secure remote execution via SSH
- Visual cron-like scheduler
- Execution logs and audit trails
- Role-based access control
- Notifications via email/Slack
- GitHub and Terraform integration

---

## ⚙️ Setup Instructions

### Backend

```bash
cd backend
python -m venv venv
source venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --reload

Frontend
cd frontend
npm install
npm run dev

⸻
🤝 Contribution Guidelines
1. Fork the repository
2. Create a new feature branch
3. Make your changes
4. Submit a pull request with a clear description
Thank you for contributing to Co-Bashi!


Deploying Co-Bashi across Azure, AWS, GCP, and on-premises involves setting up infrastructure for both the FastAPI backend and React TypeScript frontend, along with secure script execution and CI/CD. Here's a deployment guide for each platform:
⸻
☁️ 1. Azure Deployment
🔹 Backend (FastAPI)
• Use Azure App Service or Azure Container Apps
• Deploy via Docker or GitHub Actions
• Use Azure Key Vault for secrets
• Enable Managed Identity for secure access
🔹 Frontend (React)
• Use Azure Static Web Apps
• Connect to GitHub for CI/CD
• Configure routing and environment variables
🔹 Script Execution
• Use Azure VMs or Azure Kubernetes Service (AKS) for sandboxed execution
• Optionally deploy in a Trusted Execution Environment (TEE) using Azure Confidential Compute
⸻
☁️ 2. AWS Deployment
🔹 Backend
• Use AWS Elastic Beanstalk or Amazon ECS (Fargate)
• Store secrets in AWS Secrets Manager
• Use IAM roles for secure access
🔹 Frontend
• Host on AWS Amplify or S3 + CloudFront
• CI/CD via GitHub or AWS CodePipeline
🔹 Script Execution
• Use EC2 instances or EKS (Kubernetes)
• Optionally use Nitro Enclaves for TEE
⸻
☁️ 3. GCP Deployment
🔹 Backend
• Use Cloud Run or GKE (Kubernetes)
• Secrets via Secret Manager
• CI/CD via Cloud Build
🔹 Frontend
• Host on Firebase Hosting or Cloud Storage + CDN
• Integrate with GitHub for auto-deploy
🔹 Script Execution
• Use Compute Engine or GKE
• TEE via Confidential VMs
⸻
🏠 4. On-Prem Deployment
🔹 Backend
• Deploy FastAPI using Docker or Gunicorn + Nginx
• Use Vault or local secrets management
🔹 Frontend
• Serve React app via Nginx or Apache
• Use local CI/CD tools like Jenkins
🔹 Script Execution
• Use bare-metal servers or VMs
• Secure execution via SELinux, AppArmor, or containerization


Here is your downloadable ZIP file containing Terraform templates for:
• Azure
• AWS
• GCP
• On-Prem (Docker Compose)
📦 Download Co-Bashi Deployment Templates


Setting up CI/CD pipelines for Co-Bashi involves automating the build, test, and deployment processes across your environments (Azure, AWS, GCP, and on-prem). Here's a step-by-step guide using GitHub Actions, which integrates well with all platforms:
⸻
🚀 Step-by-Step CI/CD Setup with GitHub Actions
🔹 1. Create .github/workflows/deploy.yml
This file defines your pipeline. Here's a basic template:
name: Deploy Co-Bashi

on:
  push:
    branches: [main]

jobs:
  build-and-deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout code
      uses: actions/checkout@v3

    - name: Set up Python
      uses: actions/setup-python@v4
      with:
        python-version: '3.10'

    - name: Install backend dependencies
      run: |
        cd backend
        pip install -r requirements.txt

    - name: Build frontend
      run: |
        cd frontend
        npm install
        npm run build

    - name: Deploy to Azure/AWS/GCP
      run: echo "Add cloud CLI deployment commands here"

⸻
🔹 2. Add Cloud CLI Commands
Depending on your platform, add deployment steps:
✅ Azure
    - name: Azure Login
      uses: azure/login@v1
      with:
        creds: ${{ secrets.AZURE_CREDENTIALS }}

    - name: Deploy to Azure App Service
      run: |
        az webapp up --name co-bashi-backend --resource-group co-bashi-rg --location eastus

✅ AWS
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1

    - name: Deploy to ECS
      run: |
        aws ecs update-service --cluster co-bashi-cluster --service co-bashi-service --force-new-deployment

✅ GCP
    - name: Authenticate to GCP
      uses: google-github-actions/auth@v1
      with:
        credentials_json: ${{ secrets.GCP_CREDENTIALS }}

    - name: Deploy to Cloud Run
      run: |
        gcloud run deploy co-bashi-backend --image gcr.io/YOUR_PROJECT/co-bashi-backend --region us-central1

⸻
🔹 3. On-Prem Deployment
Use SSH or rsync to deploy to your local server:
    - name: Deploy to On-Prem Server
      run: |
        ssh user@your-server 'docker-compose -f /path/to/docker-compose.yml up -d'

⸻
🔐 Secrets Management
Store credentials in GitHub:
• AZURE_CREDENTIALS
• AWS_ACCESS_KEY_ID, AWS_SECRET_ACCESS_KEY
• GCP_CREDENTIALS
⸻


Here is the complete GitHub Actions CI/CD pipeline configuration for Co-Bashi, covering:
• ✅ Backend (FastAPI) build and test
• ✅ Frontend (React + TypeScript) build
• 🚀 Deployment to:
    • Azure App Service
    • AWS ECS
    • GCP Cloud Run
    • On-Prem via SSH
📄 You can download the workflow file here:
Download co_bashi_deployment_templates.zip — it includes the deploy.yml inside .github/workflows/.


To set up the required GitHub Secrets for your CI/CD pipeline, follow these steps for each cloud provider and on-prem deployment:
⸻
🔐 How to Add GitHub Secrets
1. Go to your GitHub repository.
2. Click on Settings → Secrets and variables → Actions.
3. Click New repository secret.
4. Add the following secrets:
⸻
☁️ Azure Secrets
• AZURE_CREDENTIALS: JSON string with Azure service principal credentials.
You can generate it using the Azure CLI:
az ad sp create-for-rbac --name "co-bashi-sp" --role contributor \
  --scopes /subscriptions/<SUBSCRIPTION_ID>/resourceGroups/<RESOURCE_GROUP> \
  --sdk-auth

Copy the output and paste it as the value for AZURE_CREDENTIALS.
⸻
☁️ AWS Secrets
• AWS_ACCESS_KEY_ID
• AWS_SECRET_ACCESS_KEY
Create these from the AWS IAM console by generating access keys for a user with ECS deployment permissions.
⸻
☁️ GCP Secrets
• GCP_CREDENTIALS: JSON key file for a GCP service account.
Create a service account in GCP with Cloud Run permissions, generate a key, and paste the JSON content as the secret value.
⸻
🏠 On-Prem Secrets
• ONPREM_HOST: IP or domain of your server
• ONPREM_USER: SSH username
• ONPREM_SSH_KEY: Private SSH key (paste the full key, including -----BEGIN OPENSSH PRIVATE KEY-----)
Make sure the server allows SSH access and has Docker installed.
⸻
To generate Azure credentials for GitHub Actions, follow these steps using the Azure CLI:
⸻
🔐 Step-by-Step: Generate AZURE_CREDENTIALS
✅ 1. Log in to Azure
Open your terminal and run:
az login

This opens a browser window to authenticate your Azure account.
⸻
✅ 2. Set Variables
Replace these with your actual values:
RESOURCE_GROUP="co-bashi-rg"
SUBSCRIPTION_ID=$(az account show --query id -o tsv)

⸻
✅ 3. Create a Service Principal
Run this command to generate the credentials:
az ad sp create-for-rbac \
  --name "co-bashi-sp" \
  --role contributor \
  --scopes /subscriptions/$SUBSCRIPTION_ID/resourceGroups/$RESOURCE_GROUP \
  --sdk-auth

This will output a JSON string like:
{
  "clientId": "...",
  "clientSecret": "...",
  "subscriptionId": "...",
  "tenantId": "...",
  "activeDirectoryEndpointUrl": "...",
  "resourceManagerEndpointUrl": "...",
  ...
}

⸻
✅ 4. Add to GitHub Secrets
1. Copy the entire JSON output.
2. Go to your GitHub repo → Settings → Secrets and variables → Actions.
3. Click New repository secret.
4. Name it: AZURE_CREDENTIALS
5. Paste the JSON as the value.
⸻

To generate GCP credentials for GitHub Actions, follow these steps:
⸻
🔐 Step-by-Step: Generate GCP_CREDENTIALS
✅ 1. Create a GCP Project (if you don’t have one)
gcloud projects create co-bashi-project --name="Co-Bashi"
gcloud config set project co-bashi-project

⸻
✅ 2. Enable Required APIs
gcloud services enable run.googleapis.com
gcloud services enable iam.googleapis.com

⸻
✅ 3. Create a Service Account
gcloud iam service-accounts create co-bashi-deployer \
  --display-name "Co-Bashi GitHub Actions Deployer"

⸻
✅ 4. Assign Roles
gcloud projects add-iam-policy-binding YOUR_PROJECT_ID \
  --member="serviceAccount:co-bashi-deployer@YOUR_PROJECT_ID.iam.gserviceaccount.com" \
  --role="roles/run.admin"

gcloud projects add-iam-policy-binding YOUR_PROJECT_ID \
  --member="serviceAccount:co-bashi-deployer@YOUR_PROJECT_ID.iam.gserviceaccount.com" \
  --role="roles/iam.serviceAccountUser"

⸻
✅ 5. Generate and Download JSON Key
gcloud iam service-accounts keys create key.json \
  --iam-account=co-bashi-deployer@YOUR_PROJECT_ID.iam.gserviceaccount.com

This will create a key.json file.
⸻
✅ 6. Add to GitHub Secrets
1. Open the key.json file in a text editor.
2. Copy the entire content.
3. Go to your GitHub repo → Settings → Secrets and variables → Actions.
4. Click New repository secret.
5. Name it: GCP_CREDENTIALS
6. Paste the JSON as the value.
⸻

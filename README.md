# Flask App on Azure Container Instances (ACI)

This project demonstrates how to **containerize a Flask app with Docker**, push it to **Azure Container Registry (ACR)**, and deploy it to **Azure Container Instances (ACI)** with a public endpoint.

## 🔧 Tech Stack
- Python + Flask
- Docker
- Azure CLI (Cloud Shell)
- Azure Container Registry (ACR)
- Azure Container Instances (ACI)

## 🚀 Run Locally
```bash
# Build and run locally
docker build -t myflask:1 .
docker run -p 8000:8000 myflask:1
Visit: http://localhost:8000

**# Deploy to Azure ** 
1.Create ACR & build image:
az acr create -g <RG> -n <ACR_NAME> --sku Basic
az acr build -r <ACR_NAME> -t myflask:1 .

2.Deploy container to ACI:
az container create \
  -g <RG> -n aci-myflask \
  --image <ACR_NAME>.azurecr.io/myflask:1 \
  --dns-name-label aci-myflask \
  --ports 8000 --os-type Linux

3.Get public endpoint:
az container show -g <RG> -n aci-myflask --query ipAddress.fqdn -o tsv

**#Result**
A simple Flask app running on Azure Container Instances with a public URL.

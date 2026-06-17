## 1. Infrastructure Provisioning (Task 1)

I provisioned a secure, private enterprise container registry using the Azure CLI. 

* **Registry Name:** ovivregistry
* **Resource Group:** rg-container-labs
* **SKU Selected:** Standard
* **Region:** centralindia

### Execution Commands:
```bash
az group create --name rg-container-labs --location centralindia
az acr create --resource-group rg-container-labs --name ovivregistry --sku Standard

## 2. Environment Authentication (Task 2)

Before interacting with the registry from the local command line, I authenticated the local Docker daemon engine with the secure Azure Container Registry login server.

### Execution Command:
```bash
az acr login --name ovivregistry

## 3. Application Development & Dockerfile Architecture (Task 3)

I designed a micro-application using the Python Flask framework to serve as our lightweight production workload. To containerize this application, I constructed a structured `Dockerfile` leveraging build-layer optimization rules.

### Dockerfile Blueprint:
```dockerfile
# Use an official, minimal Python runtime as a parent image
FROM python:3.9-slim

# Set working directory inside the container
WORKDIR /app

# Copy dependency files first to leverage Docker layer caching
COPY requirements.txt .

# Install dependencies without writing cache to minimize image size
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application source code
COPY app.py .

# Expose the internal networking port
EXPOSE 5000

# Set environment variables
ENV FLASK_ENV=production

# Define the execution command
CMD ["python", "app.py"]

## 4. Local Image Build & Target Tagging (Task 4)

Using the local Docker engine runtime, I built the application package and mapped explicit semantic version tags matching our private ACR domain endpoint namespace registry pattern.

### Execution Commands:
```bash
# Build the local Docker image
docker build -t app-core:v1.0.0 .

# Tag the image matching the ACR Login Server convention
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:v1.0.0
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:latest

## 5. Image Push Transmission (Task 5)

I executed a structural push command to transmit the local cached image layers to the centralized cloud repository hosted on Azure Container Registry.

### Execution Commands:
```bash
docker push ovivregistry.azurecr.io/app-core:v1.0.0
docker push ovivregistry.azurecr.io/app-core:latest

## 6. Role-Based Access Control & Security Identity (Task 6)

To implement the cloud principle of least privilege, I activated identity-driven access rules. I enabled administrative runtime credentials to establish a secure machine-to-machine channel for image deployment workloads.

### Execution Commands:
```bash
# Toggle admin credential authorization state
az acr update --name ovivregistry --admin-enabled true

# View access keys mapping to the registry scope
az acr credential show --name ovivregistry --output table

## 7. Cloud Workload Deployment (Task 7)

To demonstrate cross-platform execution, I deployed the versioned container image directly into serverless compute architecture using Azure Container Instances (ACI).

### Execution Command:
```bash
az container create --resource-group rg-container-labs \
  --name aci-flask-web-app \
  --image ovivregistry.azurecr.io/app-core:v1.0.0 \
  --cpu 1 --memory 1.5 \
  --registry-login-server ovivregistry.azurecr.io \
  --registry-username ovivregistry \
  --registry-password "********" \
  --dns-name-label oviv-app-prod \
  --ports 5000 \
  --ip-address Public

## 8. Registry Lifecycle Optimization & Cleanup (Task 8)

To maintain cost optimization and prevent storage space allocation bloat, I ran pipeline lifecycle audits to examine repository manifests and remove stale, redundant tags.

### Execution Commands:
```bash
# List tracking image repositories
az acr repository list --name ovivregistry --output table

# Audit manifest ledger strings
az acr repository show-manifests --name ovivregistry --repository app-core --output table

# Delete rolling temporary pointer tags
az acr repository delete --name ovivregistry --image app-core:latest --yes



# Azure Container Registry & Serverless Infrastructure Deployment Lab

## 1. Registry Resource Provisioning (Task 1 & 2)
I initialized a private, secure cloud repository environment utilizing the Azure Container Registry service framework. 

### Execution CLI Commands:
```bash
# Create the targeted resource group management container
az group create --name rg-container-labs --location centralindia

# Provision the secure cloud image container registry stream
az acr create --resource-group rg-container-labs --name ovivregistry --sku Standard

# Authenticate the local Docker runtime daemon to the Azure domain endpoint
az acr login --name ovivregistry


Application Development & Dockerfile Architecture (Task 3)I designed a micro-application using the Python Flask framework to serve as our lightweight production workload. To containerize this application, I constructed a structured Dockerfile leveraging layer-caching optimization principles.
Dockerfile Blueprint:
# Use an official, minimal Python runtime as a parent image
FROM python:3.9-slim

# Set working directory inside the container
WORKDIR /app

# Copy dependency files first to leverage Docker layer caching
COPY requirements.txt .

# Install dependencies without writing cache to minimize image size
RUN pip install --no-cache-dir -r requirements.txt

# Copy the rest of the application source code
COPY app.py .

# Expose the internal networking port
EXPOSE 5000

# Set environment variables
ENV FLASK_ENV=production

# Define the execution command
CMD ["python", "app.py"]

# Build the local Docker image layers
docker build -t app-core:v1.0.0 .

# Tag the image matching the ACR Login Server convention
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:v1.0.0
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:latest


Local Image Build & Target Tagging (Task 4)
Using the local Docker engine runtime, I compiled the application source assets into an immutable base image and mapped versioned semantic tags matching our private ACR cloud namespace routing patterns.
Execution Commands:
# Build the local Docker image layers
docker build -t app-core:v1.0.0 .

# Tag the image matching the ACR Login Server convention
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:v1.0.0
docker tag app-core:v1.0.0 ovivregistry.azurecr.io/app-core:latest

Image Push Transmission & Access Control (Task 5 & 6)
I executed structured push commands to transmit the compiled local image layers to the centralized cloud repository hosted on Azure. To implement the cloud security principle of least privilege, I activated administrative machine credentials to establish a secure channel for continuous deployment operations.
Execution Commands:
# Transmit the versioned asset layers to the cloud registry
docker push ovivregistry.azurecr.io/app-core:v1.0.0

# Activate the administrative access authorization security key state
az acr update --name ovivregistry --admin-enabled true

# View access keys mapping to the registry scope
az acr credential show --name ovivregistry --output table

Cloud Workload Deployment & Verification (Task 7)
To demonstrate serverless architectural capabilities, I activated the Microsoft.ContainerInstance provider and deployed our live versioned container image directly into serverless compute architecture using Azure Container Instances (ACI).
Execution Command:
az container create --resource-group rg-container-labs \
  --name aci-flask-web-app \
  --image ovivregistry.azurecr.io/app-core:v1.0.0 \
  --cpu 1 --memory 1.5 \
  --registry-login-server ovivregistry.azurecr.io \
  --registry-username ovivregistry \
  --registry-password "********" \
  --dns-name-label oviv-app-prod \
  --ports 5000 \
  --ip-address Public \
  --os-type Linux
Deployment State: Verified. The instance successfully routes incoming HTTP traffic on port 5000 via its public Fully Qualified Domain Name (FQDN) endpoint.


Registry Lifecycle Optimization & Cleanup (Task 8)
To practice structural cost optimization and prevent storage space allocation bloat, I ran pipeline lifecycle audits to examine repository manifests and permanently removed the rolling temporary latest pointer tag.
Execution Commands:
# List tracking image repositories
az acr repository list --name ovivregistry --output table

# Audit manifest hash strings
az acr repository show-manifests --name ovivregistry --repository app-core --output table

# Delete rolling temporary pointer tags safely
az acr repository delete --name ovivregistry --image app-core:latest --yes

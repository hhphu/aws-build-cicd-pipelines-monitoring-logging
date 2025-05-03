#Kubernetes Deployment

## Deploy to Kubernetes
The steps below deploy a simple Kubernetes application using GitHub Actions. Kubernetes is an open-source container orchestration platform that automates deploying, scaling, and managing containerized applications.

**Step 1 - Configure your Kubernetes Application**
Ensure your Kubernetes application has the necessary configuration files, such as Dockerfile and Kubernetes manifests (e.g., Deployment, Service, and ConfigMap).

Here is an example Dockerfile for a simple Node.js application:

```
FROM node:18
WORKDIR /app
COPY package*.json ./
RUN npm ci
COPY . .
EXPOSE 3000
CMD ["npm", "start"]
```

And an example Kubernetes Deployment manifest (deployment.yml):

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: my-k8s-app
spec:
  replicas: 1
  selector:
    matchLabels:
      app: my-k8s-app
  template:
    metadata:
      labels:
        app: my-k8s-app
    spec:
      containers:
      - name: my-k8s-app
        image: <your-container-registry>/<your-image>:latest
        ports:
        - containerPort: 3000
```

**Step 2 - Set up Kubernetes Cluster Access and Container Registry Credentials as Repository Secrets**

To securely store your Kubernetes configuration and container registry credentials, add them as encrypted secrets in your GitHub repository. Navigate to your repository's "Settings" tab, click "Secrets," and then "New repository secret."

- Add your Kubernetes configuration as a secret named KUBECONFIG.
- Add your container registry username and password as secrets named REGISTRY_USERNAME and REGISTRY_PASSWORD, respectively.

**Step 3 - Create a GitHub Actions Workflow for Deployment**
Create a new workflow file in your repository at .github/workflows/deploy.yml. This file will contain the GitHub Actions configuration for deploying your Kubernetes application.

Here's an example `deploy.yml` file:

```
name: Deploy to Kubernetes

on:
  push:
    branches:
      - main

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Set up Docker Buildx
      uses: docker/setup-buildx-action@v2

    - name: Login to container registry
      uses: docker/login-action@v2
      with:
        username: ${{ secrets.REGISTRY_USERNAME }}
        password: ${{ secrets.REGISTRY_PASSWORD }}

    - name: Build and push Docker image
      uses: docker/build-push-action@v4
      with:
        context: .
        push: true
        tags: <your-container-registry>/<your-image>:latest

    - name: Set up kubectl
      uses: azure/setup-kubectl@v2
      with:
        version: 'latest'

    - name: Deploy to Kubernetes
      run: |
        echo "${{ secrets.KUBECONFIG }}" > kubeconfig.yaml
        kubectl apply -f deployment.yml --kubeconfig=kubeconfig.yaml
```

This GitHub Actions workflow performs the following tasks:

1. Triggers the workflow on a push event to the main branch.

2. Sets up Docker Buildx on the GitHub Actions runner for building and pushing Docker images.

3. Checks out the repository.
4. Logs in to the container registry using the stored credentials.
5. Builds and pushes the Docker image to the container registry.
6. Sets up kubectl on the GitHub Actions runner.
7. Deploys the Kubernetes application using the stored Kubernetes configuration and the manifest in deployment.yml.

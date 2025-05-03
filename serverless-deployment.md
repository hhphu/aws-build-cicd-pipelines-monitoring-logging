# Serverless Deployment

Deploying an application built with the Serverless Framework using GitHub Actions will follow a similar pattern to what you have seen previously.

The Serverless Framework enables you to develop and deploy applications on various platforms such as AWS Lambda, Azure Functions, and Google Cloud Functions.

The Workflow
The following example deploys a Serverless app to AWS Lambda, but the process can be adapted for other platforms.

```
name: Deploy to AWS Lambda

on:
  push:
    branches:
      - release/*

env:
  RELEASE_NAME: ${GITHUB_REF##*release/}

jobs:
  deploy:
    runs-on: ubuntu-latest

    steps:
    - name: Checkout repository
      uses: actions/checkout@v3

    - name: Set up NodeJS
      uses: actions/setup-node@v3
      with:
        node-version: 18.x

    - name: Install dependencies
      run: |
        npm ci
        npm install -g serverless

    - name: Deploy to AWS Lambda using Serverless Framework
      run: | 
        RELEASE_NAME=${GITHUB_REF##*release/}
        serverless deploy --stage=${RELEASE_NAME}
      env:
        AWS_ACCESS_KEY_ID: ${{ secrets.AWS_ACCESS_KEY_ID }}
        AWS_SECRET_ACCESS_KEY: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
```

This GitHub Actions workflow performs the following tasks:

- Triggers the workflow on a push event to a release branch.

- Checks out the repository.

- Sets up Node.js 18 on the GitHub Actions runner.

- Installs the NodeJS dependencies and globally installs the serverless framework

- In the deploy step, first we remove a matching pattern from the GITHUB_REF environment variable.
For example, if the branch that triggered the workflow is release/v1.0.0 then the GITHUB_REF will be set to refs/heads/release/v1.0.0, and the expression *${GITHUB_REF##release/} would result in the value v1.0.0.
Then, we deploy the Serverless Framework application to AWS Lambda using the AWS credentials stored in GitHub Secrets.

With this setup, whenever you push changes to the main branch, the GitHub Actions workflow will automatically deploy your Serverless Framework application to AWS Lambda. You can modify this example to fit your specific needs or target other platforms supported by the Serverless Framework.

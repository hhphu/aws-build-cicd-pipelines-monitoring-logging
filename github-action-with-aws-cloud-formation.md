# Github Actions with AWS Cloudformation

- Cloudformation Template

```yml 

AWSTemplateFormatVersion: 2010-09-09
Description: Create an S3 bucket
Resources:
  UdaBucket:
    Type: AWS::S3::Bucket
    Properties:
      BucketName: uda-iye-bucket

      WebsiteConfiguration:
        IndexDocument: index.html
        ErrorDocument: error.html
Outputs:
  WebsiteURL:
    Value: !GetAtt UdaBucket.WebsiteURL
    Description: URL for website hosted on S3
  S3BucketSecureURL:
    Value: !GetAtt UdaBucket.DomainName
    Description: Name of S3 bucket to hold website content
```

- Workflows

```yml
# Workflow name
name: create-cloudformation-stack

# Triggers for the workflow
on:
  # Manual trigger using the workflow_dispatch event
  workflow_dispatch:
jobs: # Jobs defined in the workflow
  create-stack:
    runs-on: ubuntu-latest
    steps:
    - name: Checkout
      uses: actions/checkout@v3
   
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v2
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-session-token: ${{secrets.AWS_SESSION_TOKEN}}
        aws-region: us-east-1

    - name: Create CloudFormation Stack
      uses: aws-actions/aws-cloudformation-github-deploy@v1
      with:
        name: udatest
        template: udatest.yml
        no-fail-on-empty-changeset: "1"
        
```

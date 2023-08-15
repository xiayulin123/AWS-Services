<h1 align="center" id="title">How to set workflow</h1>

<p id="description">This is the instructions to help you setup github workflow</p>

<h2>🛠️ Installation Steps:</h2>

<p>1. make folder .github</p>

<p>2. add your workflow yml file in the folder</p>

<p>3. start writing yml</p>

<h2>🍰Guidelines:</h2>

```
name: Example workflow
on: push #wheneven someone push 

jobs: 
  run-script:
  #define which machine will run
    runs-on: ubuntu-latest
    steps:
      - name: echo a name
        run: echo "I am from Github Actions"
      - name: multiline script
        run: |-     #run multi line script
          echo "printing versions of npm and node"
          node -v
          npm -v
```
<h2>Instructions to use workflow to upload Docker Image to ECR</h2>

```
name: Deploy
on:
  push:
  #only pushed on branch main will start workflow
    branches: [ main ]
jobs:
  build:
    name: Build Image
    runs-on: ubuntu-latest
    steps:
    - name: Check out code
      uses: actions/checkout@v2
    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:

      #you can either go to Settings beside Insights -> Secrets and variables -> actions -> New repository secret
      
      #or just type it here
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: us-east-1
    - name: Login to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1
    - name: Build, tag, and push image to Amazon ECR
      env:
        ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}

        #name of ECR repo
        ECR_REPOSITORY: example_repo

        #Image tag
        IMAGE_TAG: example_IMAGE
      run: |-
        docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG .
        docker push $ECR_REGISTRY/$ECR_REPOSITORY:$IMAGE_TAG

```
# written by Yulin Xia

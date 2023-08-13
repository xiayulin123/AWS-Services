# EKS-2048
# Hi, here is the pipeline of deploying a 2048 small game into EKS in AWS


# Prerequisites (make sure you have kubectl eksctl AWS CLI helm installed if you have already installed skip this part)

# Install kubectl

##  Linux

### curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"

## MacOS

### curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"

## Windows

### curl.exe -LO "https://dl.k8s.io/release/v1.27.4/bin/windows/amd64/kubectl.exe"

## Or view instructions in https://kubernetes.io/docs/tasks/tools/

# Install eksctl

## View eksctl download instructions in https://github.com/eksctl-io/eksctl/blob/main/README.md#installation

# Install AWS CLI

## View AWS CLI install documents in https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html

# Install Helm

## Linux

### $ curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
### $ chmod 700 get_helm.sh
### $ ./get_helm.sh

## Or view Helm install documents in https://helm.sh/docs/intro/install/

# To begin:

## First: cmd aws configure 
## set up access key and region, output

## second step: to start to create a cluster 
## eksctl create cluster --name {clusterName} --region {region} --fargate
## after you see cmd says: "EKS cluster {clusterName} in {region} is ready, means your cluster has been created successfully and you can see your cluster in aws EKS

## third: download cubeconfig file get cubeCTL command line
## aws eks update-kubeconfit --name {clusterName} --region {region}

# Actual Deployment

## 1. to create fargateprofile
## eksctl create fargateprofile \
##    --cluster {clusterName} \
##   --region {region} \
##   --name {name} \
##   --namespace {namespace}
## if it's finished you can see created Fargate profile {name} on EKS cluster {clusterName}

## deploy the file of game 2048 that have all the configuration related to deployment service and ingress
## kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml


## check if the deployments are running
## kubectl get pods -n {namespace}

## after every pod are running, we can check the service 
## kubectl get svc -n {namespace}

## then we need to create ingress so that other people can see our website
## kubectl get ingress -n {namespace}


## establish a trust relationship between your AWS account and an external identity provider (IdP) that supports OpenID Connect.
## eksctl utils associate-iam-oidc-provider --cluster {clusterName} --approve

## ALB Controller
## Download IAM policy from command 
## curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json
## Or download from my git file iam_policy.json


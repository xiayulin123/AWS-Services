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
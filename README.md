# EKS-2048 🌟

<p>This project deploys the classic 2048 game on AWS using Amazon EKS.</p>

## 🚀 Prerequisites

Make sure you have the following tools installed:

- **kubectl**
  - Linux: 
    ```sh
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"
    ```
  - MacOS: 
    ```sh
    curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"
    ```
  - Windows: 
    ```sh
    curl.exe -LO "https://dl.k8s.io/release/v1.27.4/bin/windows/amd64/kubectl.exe"
    ```
- **eksctl**
  - Installation instructions: [eksctl GitHub](https://github.com/eksctl-io/eksctl/blob/main/README.md)
- **AWS CLI**
  - Installation documents: [AWS CLI Install Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- **Helm**
  - Linux:
        ```sh
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    chmod 700 get_helm.sh
    ./get_helm.sh
    ```
  - Helm installation guide: [Helm Install Guide](https://helm.sh/docs/intro/install/)

## 🛠️ Setup Steps

1. Configure AWS credentials and region:
       ```sh
   aws configure
   ```
2. Create an EKS cluster:
        ```sh
    eksctl create cluster --name {clusterName} --region {region} --fargate
    ```
3. Download kubeconfig file:
        ```sh
    aws eks update-kubeconfig --name {clusterName} --region {region}
    ```
## Actual Deployment 
1. Create Fargate Profile
        ```sh
    eksctl create fargateprofile \
    --cluster {clusterName} \
    --region {region} \
    --name {name} \
    --namespace {namespace}
    ```
2. Deploy the Game 2048
    ```sh
    kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
    ```
3. Check Deployments
    ```sh
    kubectl get pods -n {namespace}
    ```
4. Check Services
    ```sh
    kubectl get svc -n {namespace}
    ```
5. Create Ingress
    ```sh
    kubectl get ingress -n {namespace}
    ```
6. Establish Trust Relationship for OIDC
    ```sh
    eksctl utils associate-iam-oidc-provider --cluster {clusterName} --approve
    ```
## ALB Controller
1. Download IAM Policy
    ```sh
    curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json
    ```
Or download from my git file iam_policy.json
2. Create IAM Policy
    ```sh
    aws iam create-policy \
    --policy-name {policyName} \
    --policy-document file://iam_policy.json
    ```
3. Create IAM Role
    ```sh
    eksctl create iamserviceaccount \
    --cluster={your-aws-account-id}\
    --namespace= kube-system\
    --name= aws-load-balancer-controller \
    --role-name {roleName} \
    --attach-policy-arn=arn:aws:iam::{your-aws-account-id}:policy/{policyName} \
    --approve
    ```
If there is an error, try it again.

## Create Controller

1. Add Helm Repo
    ```sh
    helm repo add eks https://aws.github.io/eks-charts
    helm repo update eks
2. Install AWS Controller
    ```sh
    helm install aws-load-balancer-controller eks/aws-load-balancer-controller -n kube-system \
    --set clusterName
    ```
3. check the deployment
```shell
 kubectl get deployment -n kube-system aws-load-balancer-controller
```
wait until 2 deployments are all running

## Last check pods you can see the load balancer is running
```shell
 kubectl get pods -n kube-system
```
# Right Now your deployment is finished, you can go to AWS Load Balancer 
## to check the address
```shell
 kubectl get ingress -n {namespace}
```
## the ADDRESS is the url you can visit in the internet



## END
## Remember Delete everything you just created after you finished, Because it will cost a lot!!!!!!
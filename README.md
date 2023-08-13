# EKS-2048

This project deploys the 2048 game on AWS using Amazon EKS.

## Prerequisites

Make sure you have the following tools installed:

- `kubectl`
  - Linux: `curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/linux/amd64/kubectl"`
  - MacOS: `curl -LO "https://dl.k8s.io/release/$(curl -L -s https://dl.k8s.io/release/stable.txt)/bin/darwin/amd64/kubectl"`
  - Windows: `curl.exe -LO "https://dl.k8s.io/release/v1.27.4/bin/windows/amd64/kubectl.exe"`
- `eksctl`
  - View installation instructions: [eksctl GitHub](https://github.com/eksctl-io/eksctl/blob/main/README.md)
- AWS CLI
  - View installation documents: [AWS CLI Install Guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- Helm
  - Linux:
    ```shell
    curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/main/scripts/get-helm-3
    chmod 700 get_helm.sh
    ./get_helm.sh
    ```
  - View Helm installation guide: [Helm Install Guide](https://helm.sh/docs/intro/install/)

## Setup

1. Configure AWS credentials and region:
   ```shell
   aws configure
   ```
2. Create an EKS cluster:
   ```shell
   eksctl create cluster --name {clusterName} --region {region} --fargate
   ```
3. Download kubeconfig file:
   ```shell
   aws eks update-kubeconfig --name {clusterName} --region {region}
   ```


# Actual Deployment

## 1. Create Fargate Profile
    ```shell
        eksctl create fargateprofile \
            --cluster {clusterName} \
            --region {region} \
            --name {name} \
            --namespace {namespace}
    ```

## 2. deploy the file of game 2048 that have all the configuration related to deployment service and ingress
    ```shell
    kubectl apply -f https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/examples/2048/2048_full.yaml
    ```

## 3. check if the deployments are running
    ```shell
    kubectl get pods -n {namespace}
    ```

## 4. after every pod are running, we can check the service 
    ```shell
    kubectl get svc -n {namespace}
    ```

## 5. then we need to create ingress so that other people can see our website
    ```shell
    kubectl get ingress -n {namespace}
    ```

## 6. establish a trust relationship between your AWS account and an external identity provider (IdP) that supports OpenID Connect.
    ```shell
    eksctl utils associate-iam-oidc-provider --cluster {clusterName} --approve
    ```
# ALB Controller
## 1. Download IAM policy from command 
    ```shell
    curl -O https://raw.githubusercontent.com/kubernetes-sigs/aws-load-balancer-controller/v2.5.4/docs/install/iam_policy.json
    ```
## Or download from my git file iam_policy.json

## 2. create IAM policy using the IAM policy file
    ```shell
    aws iam create-policy \
    --policy-name {policyName} \
    --policy-document file://iam_policy.json
    ```

## 3. create the IAM role by going to AWS IAM, go into Access management -> Roles -> create the Role -> AWS account -> next -> select {policyName} -> next -> create role name and create role

## or do it in cmd:
```shell
 eksctl create iamserviceaccount \
   --cluster={your-aws-account-id}\
   --namespace= kube-system\
   --name= aws-load-balancer-controller \
   --role-name {roleName} \
  --attach-policy-arn=arn:aws:iam::{your-aws-account-id}:policy/{policyName} \
   --approve
```
## if there is an error try it one more time

# create controller 
## 1. add helm repo
```shell
helm repo add eks https://aws.github.io/eks-charts
helm repo update eks
```
## 2. install aws controller
```shell
 helm install aws-load-balancer-controller eks aws-load-balancer-controller -n kube-system \
   --set clusterName={clusterName} \
   --set serviceAccount.create=false \
   --set serviceAccount.name=aws-load-balancer-controller \
   --set region={region} \
   --set vpcId={your-vpc-id}
 vpc id is in your AWS EKS -> networking
```
## 3. check the deployment
```shell
 kubectl get deployment -n kube-system aws-load-balancer-controller
```
## wait until 2 deployments are all running

# Last check pods you can see the load balancer is running
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
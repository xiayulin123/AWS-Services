1. go to EC2 create EKS server (Amazon Linux, Linux2, t2.micro, keypair)
2. connect to EC2 by SSH (user: ec2-user)
3. switch to root
```
sudo su
```
4. change the hostname of server
```
hostname {EKS server name}
cd /etc
vim hostname
## delete the first line and leave it as:
{EKS server name}


init 6
#reboot
```
5. Download Kubectl
```
curl -O https://s3.us-west-2.amazonaws.com/amazon-eks/1.27.1/2023-04-19/bin/linux/amd64/kubectl

chmod +x ./kubectl

mv kubectl /bin
```
6. Download EKSctl
```
curl --silent --location "https://github.com/weaveworks/eksctl/releases/latest/download/eksctl_$(uname -s)_arm64.tar.gz" | tar xz -C /tmp

cd /tmp
mv eksctl /bin

```
7. Install aws-iam-authenticator (optional, but I have problem to connect eks if I didn't install this)
```
curl -Lo aws-iam-authenticator https://github.com/kubernetes-sigs/aws-iam-authenticator/releases/download/v0.5.9/aws-iam-authenticator_0.5.9_linux_amd64
chmod +x ./aws-iam-authenticator
mv aws-iam-authenticator /bin

```
8. go to aws IAM -> create Role -> Add policy -> AWSCloudFormationFullAccess, IAMFullAccess, AmazonEC2FullAccess, AdministratorAccess -> create role ->go to ec2 -> change the role of your eks server to the role just created

9. go back to server
```
eksctl create cluster --name {cluster name} --region {your region} --node-type {size} --nodes 2

kubectl get nodes
## if you have error with api stuff better check if you have installed aws-iam-authenticator 
## and redo the steps from step 1

vim deployment.yml
## look the deployment.yml in repo
vim service.yml
## look the service.yml in repo
```

10. Integrate EKS with Ansible
```
vim /etc/ssh/sshd_config

#change the passwordAuthentication to yes

passwd root
service sshd reload

```

11. go to ansible server
```
sudo vim /etc/ansible/hosts
## look at hosts file in repo folder
## add another host

ssh-copy-id root@{EKS private ip address}
## so that each time connect to eks server will automatically access the key 
ssh root@{EKS private ip address}

vim kubectlDeploy.yml
## look at kubectlDeploy.yml in repo folder

ansible-playbook kubectlDeploy.yml
## rerun the file
```

12. go back to eks server
```
kubectl get pods

## your should see 2 pods are running 

kubectl get all

## you can see your loadbalance is ruuning and listen to External-IP and you can go to that ipadress:port

```

Everything is finished!
Congradulations you have complete CI/CD Project!
1. go to EC2 create Ansible server (Amazon Linux, Linux2, t2.micro, keypair)
2. connect to EC2 by SSH (user: ec2-user)
3. switch to root
```
sudo su
```
4. change the security group of instance, ad inbound rule of 8080-8090 port source anywhere
5. change the hostname of server
```
hostname {Ansible server name}
cd /etc
vim hostname
## delete the first line and leave it as:
{Ansible server name}
```
6. reboot server
```
init 6
```
7. reconnect switch to root
8. create user
``` 
useradd {user}
passwd {user}
New password: {password}

visudo
##change the file as visudo file(add {user} near to the end)

vim /etc/ssh/sshd_config
##change the file as sshd_config gile (change password authntication from no to yes)

service sshd reload
```

9. switch to {user}
```
sudo su - {user}

```
10. for next part that connect Ansible with EKS Boot server, generate public key in this server
```
ssh-keygen
(all default)
```
11. check if the key generated
```
ls ~/.ssh

##you should see id_rsa.pub and id_rsa
```

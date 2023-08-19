1. go to EC2 create Jenkins server (Amazon Linux, Linux2, t2.micro, keypair)
2. connect to EC2 by SSH (user: ec2-user)
3. sudo su
4. download Jenkins
5. change the hostname of server
```
hostname {Jenkins server name}
cd /etc
vim hostname
## delete the first line and leave it as:
{Jenkins server name}
```

6. reboot server
```
init 6
```
7. change the security group of instance, ad inbound rule of 8080 port source anywhere
8. go to public ip address:8080 to unlock Jenkins
```
## password is in jenkins instance
cat /var/lib/jenkins/secretes/initialAdminPassword
```
9. Install suggested plugins

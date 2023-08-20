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
12. install ansible
```
sudo su
amazon-linux-extras install ansible2

##check
ansible --version

```
13. Integrate ansible with Jenkins
Jenkins Dashboard ->  manage Jenkins -> system ->  publish over SSH(plug in) -> Add SSH Server -> Name: {ansible server name} Hostname: {ansible server public ip address} Username: {user} -> Advanced -> mark Use password authentication -> Password: {password} -> apply -> Test configuration (if is success) ->  save

14. Go to Ancible server, create a Docker dir
```
cd /opt

sudo mkdir Docker

sudo chown {user}:{user} Docker
## give {user} permmision to access Docer so that Jenkins can modify and change Docker file
## you can check with command ll


```

15. Go to Jenkins -> create new item -> {item name}, Maven project -> Git repository URL (enter your github repo URL) -> branch: {branch} -> Build Goals and options: clean install -> Post-build Actions    Add post-build action: Send build artifact over SSH -> Server name: {ansible server name}, source file: /path/to/your/*.war, Remove prefix: /path/to/your -> apply -> save

16. go to configure -> Remote directory: //opt//Docker -> apply -> save

17. click on the Item you create just now -> Build Now

18. check the console output if it's success by the end

19. go to ansible server
```
ls Docker/

## your should see {your file}.war
## your jenkins has successfully connect with your ansible server
## the artifacts is successfully published into your ansible server
```

20. configure and install Docker
```
sudo yum install docker

sudo usermod -aG docker {user}
## to add {user} to docker group, give access to docker
## you can check with id {user}

sudo service docker start

service docker status(check if running)

sudo init 6
## reboot

sudo service docker start
sudo su - {user}
cd /opt/Docker

vim Dockerfile
```
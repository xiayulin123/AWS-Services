1. go to EC2 create Jenkins server (Amazon Linux, Linux2, t2.micro, keypair)
2. connect to EC2 by SSH (user: ec2-user)
3. switch to root
```
sudo su
```
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
10. create admin user
11. go to jenkins server
```
sudo su
## go to https://maven.apache.org/download.cgi copy the Binary tar.gz archive link address
cd /opt
wget {Binary tar.gz archive link address}
tar -xzvf {file}.tar.gz
mv {file} maven

## set environmen variable of maven
cd ~
ll -a

## find java file path
find / -name java-11*
## copy the address of /usr/lib/jvm/java-11-openjdk-{version}
vim .bash_profile
## look .bash_profile in repo
```
12. check settings
```
source .bash_profile
echo $PATH
mvn -v
```
13. go to public ip address:8080 and login
14. Manage Jenkins -> plugins ->  install maven integration without restart -> install SSH plugin (to ensure the SSH connect you can install all SSH plugins)
15. Manage Jenkins -> Tools -> Add JDK name:java11  JAVA_HOME: /usr/lib/jvm/{java file} ## the warning
16. Tools -> Maven -> Add Maven Name:maven -> unmark the install automaticlly -> MAVEN_HOME: /opt/maven    ->  Apply  ->  Save
17. Manage Jenkins -> Plugins -> installed plugins -> disable Github branch source plugin -> enable Github plugin -> click restart once no ...
18. Go to Jenkins server
```
sudo su
yum install git
```
19. since now it has successfully set up, you can create item to test maven build

Next -> Ansible folder
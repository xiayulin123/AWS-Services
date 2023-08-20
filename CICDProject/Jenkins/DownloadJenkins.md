Ensure that your software packages are up to date on your instance by using the following command to perform a quick software update:

[ec2-user ~]$ sudo yum update –y

Add the Jenkins repo using the following command:

[ec2-user ~]$ sudo wget -O /etc/yum.repos.d/jenkins.repo \
    https://pkg.jenkins.io/redhat-stable/jenkins.repo

Import a key file from Jenkins-CI to enable installation from the package:

[ec2-user ~]$ sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io-2023.key
[ec2-user ~]$ sudo yum upgrade

Install epel:
amazon-linux-extras install epel

Install Java (Amazon Linux 2):

[ec2-user ~]$ sudo amazon-linux-extras install java-openjdk11 -y

Install Java (Amazon Linux 2023):

[ec2-user ~]$ sudo dnf install java-11-amazon-corretto -y

Install Jenkins:

[ec2-user ~]$ sudo yum install jenkins -y

Enable the Jenkins service to start at boot:

[ec2-user ~]$ sudo systemctl enable jenkins

Start Jenkins as a service:

[ec2-user ~]$ sudo systemctl start jenkins

If you are finished check:
$javac --version
javac .....

$systemctl status jenkins
running...
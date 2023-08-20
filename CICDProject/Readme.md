<h2>Here are the CICD steps that this project will go through </h2>

<h2>🛠️ CI Steps:</h2>

<p>1. changes in github repo</p>

<p>2. initiate the job trigger</p>

<p>3. Jenkins pull the code from repo</p>

<p>4. build the artifact using maven</p>

<p>5. push the artifact to ansible server</p>

<p>6. create docker image using artifact</p>

<p>7. copy the docker image to docker hub</p>

<h2> Continue to CD Steps </h2>

<p>1. boost server pull docker image from dockerhub</p>

<p>2. build container for kubernetes</p>

<p>3. finished</p>

<h2> To see details please click link below or head into Jenkins folder </h2>

## [Continue to the details](https://github.com/xiayulin123/AWS-Services/tree/main/CICDProject/Jenkins)

# Demo

## Project
![project](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo1.png)

## JenkinsDashBoard
![JenkinsDashBoard](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/JenkinsDashboard.png)

## JenkinsCD
![JenkinsCD](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/JenkinsCDJob.png)

## JenkinsCI
![JenkinsCI](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/JenkinsCIJob.png)

## EC2 final look
![EC2 final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/AWSEC2.png)

## EKS final look
![EKS final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/AWSEKS.png)

## Dockerhub final look
![Dockerhub final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/Dockerhub.png)

## EKSBootRole
![EKSBootRole](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/EKSBootRole.png)

## all k8s service
![all k8s service](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/allK8sServer.png)

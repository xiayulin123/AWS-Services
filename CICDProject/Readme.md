<h2>Here are the CICD steps that this project will go through </h2>

<h2>🛠️ CI Steps:</h2>

<p>1. Changes in github repo</p>

<p>2. Initiate the job trigger</p>

<p>3. Jenkins pull the code from repo</p>

<p>4. Build the artifact using maven</p>

<p>5. Push the artifact to ansible server</p>

<p>6. Create docker image using artifact</p>

<p>7. Copy the docker image to docker hub</p>

<h2> Continue to CD Steps </h2>

<p>1. Boost server pull docker image from dockerhub</p>

<p>2. Build container for kubernetes</p>

<p>3. Finished</p>

<h2> To see details please click link below or head into Jenkins folder </h2>

## [Continue to the details](https://github.com/xiayulin123/AWS-Services/tree/main/CICDProject/Jenkins)

# Demo

## Project
![project](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/demo1.png)

## JenkinsDashBoard
![JenkinsDashBoard](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/JenkinsDashboard.png)

## JenkinsCD
![JenkinsCD](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/JenkinsCDJob.png)

## JenkinsCI
![JenkinsCI](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/JenkinsCIJob.png)

## EC2 final look
![EC2 final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/AWSEC2.png)

## EKS final look
![EKS final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/AWSEKS.png)

## Dockerhub final look
![Dockerhub final look](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/Dockerhub.png)

## EKSBootRole
![EKSBootRole](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/EKSBootRole.png)

## all k8s service
![all k8s service](https://github.com/xiayulin123/AWS-Services/blob/main/CICDProject/demo/allK8sServer.png)

# Configuring Docker logs to AWS CloudWatch
Here is a simple example on configuring docker container logs to the AWS CloudWatch

# Docker
Docker is an open platform for developing, shipping, and running applications. Docker enables you to separate your applications from your infrastructure so you can deliver software quickly. 

Docker provides the ability to package and run an application in a loosely isolated environment called a container. The isolation and security allow you to run many containers simultaneously on a given host. Containers are lightweight and contain everything needed to run the application, so you do not need to rely on what is currently installed on the host. You can easily share containers while you work too.
You can learn more about the same in the [website.](https://docs.docker.com/get-started/overview/)

# What Is a Container
A container is a standard unit of software that packages up code and all its dependencies so the application runs quickly and reliably from one computing environment to another. Docker container image is a lightweight, standalone, executable package of software that includes everything needed to run an application: code, runtime, system tools, system libraries and settings.
You can learn more about the same in the [website.](https://www.docker.com/resources/what-container)

# Installing Docker
> Here I am using AWS Amazon linux server
```sh
amazon-linux-extras install docker -y
systemctl restart docker.service
systemctl enable docker.service
```
Please see the [website](https://docs.docker.com/engine/install/) for more information.

# CloudWatch
CloudWatch provides you with data and actionable insights to monitor your applications, respond to system-wide performance changes, optimize resource utilization, and get a unified view of operational health. CloudWatch collects monitoring and operational data in the form of logs, metrics, and events, providing you with a unified view of AWS resources, applications, and services that run on AWS and on-premises servers.
You can learn more about the same in the [website.](https://aws.amazon.com/cloudwatch/)

# Steps to follow - A Simple Example
- Open CloudWatch Logs in the Management Console.
- Create a log group name docker-logs (with any name)
- Go to IAM and create a role for the use with EC2 named docker-logs and attach the CloudWatchLogsFullAccess policy. 
> Note: do not use the CloudWatchLogsFullAccess policy for production workloads. Restrict access to the specific resource and actions instead.
- Select the IAM role ‘docker-logs’(the name provided) and attach to the EC2 Instance.
- Install docker in the Instance.
- Start a container as below or as per your requirement
```sh
docker run -d \
--log-driver=awslogs \
--log-opt awslogs-group=docker-logs \  ##==> Your log name
-p 80:80 \
nginx:latest
```
- Open your CloudWatch Logs group to find your log message.

# Conclusion
Here we are configuring docker container logs to the AWS CloudWatch.

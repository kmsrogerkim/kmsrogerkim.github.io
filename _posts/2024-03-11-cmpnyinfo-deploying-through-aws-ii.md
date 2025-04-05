---
layout: single
title: "cmpnyinfo: deploying through aws II"
categories: cmpnyinfo
tag: [aws, ecs]
---
### Subtitle: the basics of ECS

## Introduction

In this post, I am going to talk about
1. What AWS's Elastic Container Service(ECS) is
2. How it operates
3. Some key terms

## What is ECS?

Amazon Web Services(AWS) provides its own managed container orchestrator called Elastic Container Service(ECS).

### What is a container orchestrator?

Managed container orchestrator, like Kubernetes, or ECS, is a form of service that is responsible for
1. fininding available infrastructures, like servers, EC2 instances
2. Creating, Starting and Destroying containers accordingly
3. deploying application across multiple servers/instances through containers
4. autoscaling
5. many more...

### Back to ECS

ECS is rather a simple alternative to more sophisticated and complex container orchestrators like Kubernetes. You can easily deploy your containerized application across your servers, either with the GUI provided by the AWS, or even through few simple API calls!

## Key terms
- **Launch Type**: either Fargate or EC2.
    - There are more configurations you have to do for EC2 launch type. Like network modes.
    - You can run containers without the need to directly provision or manage EC2 instances.
- **Clusters**: the underlying physical resources that your containerized application is going to run on. 
    - e.x: EC2 instances
- **Task Definition**: it's easy to understand when you think of it as the ECS equivalent of docker-compose file. A set of instructions about how each containers should be deployed.
- **Task**: the running process of what was defined in the task definition.
- **Service**: your service. The running tasks form a service.
    - Ensures that a certain number of tasks are running.

## Diagram
![](/assets/img/ecs-struct.png)
1. You upload the images you created to Elastic Container Registry(ECR)
    - Don't worry I will cover this part in more detail in the next post
2. You create your task definition through ECS
    - The task definition can be represented as a json file
    - Containing info such as container name, port configurations, networkmode,
3. The ECS deploys the task to the underlying infrastructures in the cluster
    - Tasks will form according to the task definition you wrote

## Contact Me:

Roger Kim

[Github](https://github.com/kmsrogerkim)


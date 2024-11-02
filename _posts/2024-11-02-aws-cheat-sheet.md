---
layout: single
title: "Everything You Have to Know about AWS"
categories: aws
tag: [back-end, aws] 
---
## Introduction 
In this post, I am going to explain some of the core services provided by aws
- awscli
- VPC 
- EC2
- ELB 
- RDS
- S3, ECS, ECR
- route53 & Hosting Zone

## awscli (AWS Command Line Interface)
One thing that needs to be kept in mind, is that almost everything you do in AWS management console, the website through GUI, can be done in awscli. Writing tesk definitions, deploying ecs, you name it. However, in order to get started, you have to set it up first. 
I have talked about the **detailed steps of creating an IAM user, and configuring your awscli in terminal** in my [cmpnyinfo: deploying through aws III(fin)](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-deploying-through-aws-iii-fin/). However, I just want to add one thing. Which is creating and managing multiple profiles in your awscli. You can configure a new profile using

- `aws configure --profile profile_name`

Then, you can use that profile by putting `--profile profile_name` at the end of the command. For example
- `aws login --profile my_profile`

## VPC (Virtual Private Cloud)
I personally think that the VPC is the most important concept you have to know in AWS. Imagine it as a room where you put your servers/services in, such as your DB, EC2 instance, and so on. Just like LAN(Local Area Network), the computers inside the room can freely communicate with each other, and you have to set up your internet connection to the outside world (Gateways). You can set up public and private subnets, and those in private subnets cannot be accesed from the outside world. Please mind that these are metaphors to help you understand, not technical explanation.

It is important to set up your vpc before anything (EC2, ECS, RDS, ELB and so on) since later on, you will be connecting and forwarding your traffics through route53 to your VPC. It is important to place all your resources for your service inside one VPC.

For example, let's say I want to launch a simple django application using AWS. The general workflow would look something like this.
- Set up VPC and SG
- Place my DB, either using RDS or running in EC2, in my private subnet, since I do not want it to be accessible from the outside world
- Configure the DB setting in my Django accordingly for my DB
- Create a docker image for my Django application
- Upload it to ECR
- Lauch using ECS or EC2, which will also be placed in my VPC's public subnet
- Set up hosted zone in route53
- Create target group for my Django running in VPC
- Create ALB and connect it to the target group
- Connect ALB to the hosted zone and register domain, SSL certificates

In the example above, my Django application can freely access my DB in private subnet since they are in the same VPC, but anybody outside the VPC can't make any requests to my DB. I can't even directly SSH into it from my PC. There are some key concepts of VPC that you should understand. They are Subnets, Gateways and CIDR ranges.

### Subnets


## EC2
EC2 is perhaps the most foundational and fundamental aws service. You can basically borrow a computer from aws, set it up and run your servers there.
talk abuot setting it up

## ELB (Elastic Load-Balacer)

## RDS (Relational Database Service)

## S3, ECS and ECR
### S3
S3 are buckets that store you data. You can either make it public or private. To use it in django, you have to have these thigns
### ECS (Elastic Container Service)
It lets you deploy you application using images you build. It is very easy to launch and deploy. It will also configure the networking settings for you.
### ECR (Elastic Container Registry)
It is basically where you can store your docker images.

## Contact Me:
Roger Kim

[Github](https://github.com/kmsrogerkim)

e-mail: <minseungkim1017@gmail.com> 
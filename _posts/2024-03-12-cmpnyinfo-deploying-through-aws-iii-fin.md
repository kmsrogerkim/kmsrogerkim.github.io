---
layout: single
title: "cmpnyinfo: deploying through aws III(fin)"
categories: cmpnyinfo
tag: [aws, ecs]
---
### Subtitle: uploading image to ecr; deploying with ecs

## Introduction

In this post, I am going to talk about
1. uploading the docker image to ECR
2. creating cluster in ECS
3. writing task definition for my cmpnyinfo application
4. creating service & deploying with ECS

## Uploading to ECR

I am going to explain how I setup awscli in my Ubuntu WSL. This should work just fine even if you are just using Ubuntu that's not WSL.

***First,*** you have to create an user in the IAM console. Create an access key and set the policies for Public&Private registry.

***Secondly,*** type the command `sudo apt install awscli` to install awscli  
- If this give you an error, try typing: 
- `pip install 'urllib3<2'`

***Thirdly,*** type the command `aws configure`; and configure your settings accordingly.
- You can type `aws configure list` to see all the configurations of the profiles you created

***Lastly,*** copy the commands in provided by ECR when you push the `View push commands` button. It should look something like this
![](/assets/img/ecr-push-commands.jpg)

- If you facen and error, configure the **~/docker/config.json** file and delete this line
```
"credStore": "desktop"
```     
- The full code would look sth like this
```
{
  "auths": {
    "https://index.docker.io/v1/": {},
    "public.ecr.aws": {
      "auth": "some-stuff
    }
  }
}
```
***Mind the comma! Make the code compiable!*** 

## Creating cluster

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
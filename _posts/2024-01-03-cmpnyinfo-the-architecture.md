---
layout: single
title: "cmpnyinfo: the architecture"
categories: cmpnyinfo
---

## Introduction

I usually like to plan things through before I do it. Especially if I am working on a project like this. And there is a literal study revolving how to make a software, called _software architecture._ I am not exactly an expert in this field. But I tried to apply some concepts from it, on the process of planning how to design my website.

## Software Architecture Pattern

There are several software architecture patterns, which I am not going to explain in this post (maybe in a seperate post later). But I am going to explain what pattern I chose to use for my website. It's ***modular monolithic architecture.***

**What is modular monolithic architecture?**

According to my friend, GPT, it is basically when you 
1. seperate parts of your software into differnet _modules_ that does certain things
2. and those _modules_ are all built in one giant monolithic service, in this case, an EC2 instance.

Now if you ask me what exactly this _module_ stands for, I have no idea. That's what I'm wondering as well.

## How it applies to my website

This architecture, in my opinion, suits bests to my website, for the following reasons.

- **It is simple**
    - My website doesn't really have a lot of features. And I am not planning to make it that way.
    - So putting everything together in a monolithic instance wouldn't cause a huge mess.
    - I don't have to take an extra step and use the AWS's ECS service to manage different EC2 container instances. Since I am just running one EC2 instance.
    - As a result, simpler design! Less complexity!
- **A certain level of seperation**
    - When you look at the _diagram below_, you can see how the API _module_ and the Web-app _modules_ has their own data to access.
    - It is not exactly seperated in terms of having a seperate database, or a seperate server, or instance for it, ***BUT*** I am planning not to write a single line of code that accesses those data of other application. This way, they are seperated.

**Diagram** 
![diagram](/assets/img/cmpnyinfo_architecture.png)

# Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
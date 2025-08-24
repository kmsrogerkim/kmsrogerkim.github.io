---
title: "About"
layout: single
permalink: /about/
author_profile: true
sidebar_main: true
---
# Minseung (Roger) Kim 
[![GitHub](https://img.shields.io/badge/GitHub-181717?logo=github&logoColor=white)](https://github.com/kmsrogerkim) [![LinkedIn](https://img.shields.io/badge/LinkedIn-0A66C2?logo=linkedin&logoColor=white)](https://www.linkedin.com/in/kmsrogerkim/)  

Welcome! I am Roger Kim, a computer science student at [Hanyang University](https://www.hanyang.ac.kr/web/eng), Seoul. With expertise in Python and experience in C, C++, Java and JS, I Have built several REST APIs using **Django REST Framework (DRF)**. 

I am familiar with essential deploying tools such as Docker, AWS, GitHub Actions and so on.
Furthermore, I am experienced in team working and is experienced with agile culture that I have learnt while being part of a startup project.

## Experience
### Student Researcher (Oct 2024 - July 2025)
- Prof. Jin's [Vibro-Acoustics Medical Lab](https://vibroacoustic.imweb.me/) at HYU
- Integrated ***Machine Learning*** and ***Digital Signal Processing*** techniques to develop an automated cough counting and segmentation system.

## Key Skills
### Software Engineering
- Backend development with ***Django***
- REST API development with ***Django Rest Framework (DRF)***
- Containerization with ***Docker***
- Deploying with ***AWS*** (ECS, EC2, RDS, Lambda, and more.)

### Machine Learning
- ***Computer Vision***
- ***ML*** in ***Digistal Signal Processing***
- Shipping Models with ***ONNX***

## Projects

### Cough Segmentation
---

<p float="left">
  <img src="/assets/img/SLab.png" width="100%" />
  <img src="/assets/img/cough_counting_process.png" width="100%" />
  <img src="/assets/img/segmented_cough.png" width="100%" />
</p>

I worked on the [Development of Respiratory Disease Diagnosis Model Based on Cough Sounds](https://vibroacoustic.imweb.me/current/?q=YToxOntzOjEyOiJrZXl3b3JkX3R5cGUiO3M6MzoiYWxsIjt9&bmode=view&idx=22761988&t=board), when I was participating at the [Vibro-Acoustics Medical Lab](https://vibroacoustic.imweb.me/) at HYU. Integrated ***Computer Vision Model*** and ***DSP Algorithm*** together for Automated Cough Counting & Segmentation.

### Contributions
- Shipped DL models with **DRF** & **ONNX**
- Deployed on **AWS**
- **Minimized Docker Image for DL Models**
- Developed DSP algorithm with **Python**

### Clip
---

<p float="left">
  <img src="/assets/img/about/clip_landing.png" width="100%" />
</p>

[Clip](https://www.clipclub.co.kr/) provides customizable tools that allow any university club to build its own system based on its unique way of operating. By doing so, it automates repetitive administrative tasks, enhances collaboration efficiency, and improves the participation experience for all members.

### Contributions
- Managed domains with **Route53**, configuring subdomains
- Deployed static pages using **CloudFront + S3**
- **Containerized** applications with **Docker** to deploy to **AWS EC2 instances**: 
  - Flask servers, Flutter web apps, React & Next.js frontends
- Designed overall software architecture, including URL redirection and service routing logic

### TOYKI
---

<p float="left">
  <img src="/assets/img/toyki-homepage.png" width="100%" />
</p>

[TOYKI](https://toyki-homepage.vercel.app/) is a service that provides opportunities to overcome the limitations of offline human relationships and enables everyone to build social networks more easily. It was a startup project that was done under the [Hanyang Institute for Entrepreneurship (한양대 창업지원단)](https://startup.hanyang.ac.kr/en). The project was elected as a finalist in the 2024 [Student Startup Promising Team 300+ Competition](https://u300.kr/)


### Contributions
- Frontend development with React
- Built REST API with **Django Rest Framework**
- Containerized and deployed with **Docker**, **AWS ECS**
- Set up & managed DB with **PostgreSQL** running on **AWS RDS**

### Related Articles

#### AWS
- [AWS VPC Crash Course](https://kmsrogerkim.github.io/aws/aws-vpc/)
- [Basic IAM Features](https://kmsrogerkim.github.io/aws/aws-basic-iam-features/)

#### DRF
- [Customize DRF Simplejwt](https://kmsrogerkim.github.io/python/customize-opensource/)
- [Introduction to Django Rest Framework](https://kmsrogerkim.github.io/django/django-intro-to-drf/)
- [JWT feat. Django](https://kmsrogerkim.github.io/django/jwt/)
- [Understanding DRF's Serializer](https://kmsrogerkim.github.io/django/django-drf-serializers/)

#### DevOps
- [Dependency Management with Poetry](https://kmsrogerkim.github.io/python/python-dependency-management-with-poetry/)
- [Github Actions to Automate Image Pushing & Django Testing](https://kmsrogerkim.github.io/devops/github-actions/)


## Personal Projects

### cmpnyinfo
---
<p float="left">
  <img src="/assets/img/about/cmpnyinfo_porfolio_unified.png" width="100%" />
</p>

This is a simple website that analyses the financial statements of corporations registered in Korean Composite Stock Price Indexes(KOSPI). It provides ***essential analytical data*** and ***visual representation*** using variouse types of graphs.

**Tech Stack**
- Pure HTML & CSS for front
- **Django** for back
- **Docker** and **AWS ECS** for deployment

### NAVER Shopping Insight
---
<p float="left">
  <img src="/assets/img/naver1.png" width="95%" />
  <img src="/assets/img/naver2.png" width="95%" />
</p>

Visit it [here](https://github.com/kmsrogerkim/NAVER-Shopping-Insight). 
This is an API-based application that gathers information such as, 
1. the most searched keywords for shopping categories, from one of South Korea's biggest IT company, NAVER.
2. other such as monthly searched numbers, product numbers, competition index, etc.

**⚙️ Packages Used**
- **`pandas`**, and more.

### Corporate Analysis
---

<p float="left">
  <img src="/assets/img/corporate_analysis1.png" width="95%" />
  <img src="/assets/img/corporate_analysis2.png" width="95%" />
</p>

Visit it [here](https://github.com/kmsrogerkim/PYTHON-Corporate-Data-Analysis).

This opensource, API-based project:
1. gathers & organizes the financial statements of companies listed in KOSPI(Korean Composite Stock Price Index); over the period of past six years.
2. calculates essential & meaningful ***analytical data***. For example:
    - ROA, ROE, PER, 
    - Revenue/Operating Income/Net Income increase rate
    - Profit Status
3. visualizes those datas in various types of graphs. (Box plot, scatter plot, etc)

**Packages Used**

- **Financial Data Retrieval**
  - `OpenDartReader` ***(API)***
  - `FinanceDataReader`

- **Data Analysis & Manipulation**
  - `pandas`
  - `numpy`

- **Others**
  - `pytest`
  - `pickle`

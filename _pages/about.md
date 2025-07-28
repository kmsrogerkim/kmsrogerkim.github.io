---
title: "About"
layout: single
permalink: /about/
author_profile: true
sidebar_main: true
---
# Minseung (Roger) Kim

Welcome! I am Roger Kim, a computer science student at [Hanyang University](https://www.hanyang.ac.kr/web/eng), Seoul. With expertise in Python and experience in C, C++, Java and JS, I Have built several REST APIs using **Django REST Framework (DRF)**. 

I am familiar with essential deploying tools such as Docker, AWS, GitHub Actions and so on.
Furthermore, I am experienced in team working and is experienced with agile culture that I have learnt while being part of a startup project.

## Key Skills
### Software Engineering
- Backend development with ***Django*** & ***Django Rest Framework***
- Containerization with ***Docker***
- Deploying with ***AWS*** (ECS, EC2, RDS, Lambda, and more.)

### Machine Learning
- ***Computer Vision*** (Object Detection, Classification)
- ***ML*** with ***Digistal Signal Processing***
- Shipping DL Models with ***ONNX***

## Experience
### Student Researcher (Oct 2024 - July 2025)
- Prof. Jin's [Vibro-Acoustics Medical Lab](https://vibroacoustic.imweb.me/) at HYU
- Integrated ***Computer Vision Model*** into ***DSP Algorithm*** for Automated Cough Counting & Segmentation

## Projects
## Cough Segmentation
<p float="left">
  <img src="/assets/img/SLab.png" width="100%" />
  <img src="/assets/img/cough_counting_process.png" width="100%" />
  <img src="/assets/img/segmented_cough.png" width="100%" />
</p>

I worked on the [Development of Respiratory Disease Diagnosis Model Based on Cough Sounds](https://vibroacoustic.imweb.me/current/?q=YToxOntzOjEyOiJrZXl3b3JkX3R5cGUiO3M6MzoiYWxsIjt9&bmode=view&idx=22761988&t=board), when I was participating at the [Vibro-Acoustics Medical Lab](https://vibroacoustic.imweb.me/) at HYU. Integrated ***Computer Vision Model*** and ***DSP Algorithm*** together for Automated Cough Counting & Segmentation.

### Tech Stack
- **AWS** for deployment
- **DRF** & **ONNX** for shipping DL Models
- **Minimizing Docker Image for DL Models**
- **Python** for DSP algorithms (eg. librosa)

## TOYKI
<p float="left">
  <img src="/assets/img/toyki-homepage.png" width="100%" />
</p>

[TOYKI](https://toyki-homepage.vercel.app/) is a service that provides opportunities to overcome the limitations of offline human relationships and enables everyone to build social networks more easily. It is currently under development, and I am developing Backend API. Learn more about [TOYKI here](https://toyki-homepage.vercel.app/): https://toyki-homepage.vercel.app/


### Tech Stack
- React
- **DRF** for REST API
- **Docker** for containerization
- **ECS** for deployment
- **PostgreSQL** on **RDS** for DB

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


## Fun Little Projects
### cmpnyinfo
<p float="left">
  <img src="/assets/img/cmpnyinfo_portfolio_detail_eng.png" width="49%" />
  <img src="/assets/img/cmpnyinfo_portfolio_main.png" width="50%" /> 
</p>
This is a simple website that analyses the financial statements of corporations registered in Korean Composite Stock Price Indexes(KOSPI). It provides ***essential analytical data*** and ***visual representation*** using variouse types of graphs.

**Tech Stack**
- pure html&css for front
- **Django** for back
- **Docker** for containerization
- **ECS** for deployment

### NAVER Shopping Insight
<p float="left">
  <img src="/assets/img/naver1.png" width="95%" />
  <img src="/assets/img/naver2.png" width="95%" />
</p>
Visit it [here](https://github.com/kmsrogerkim/NAVER-Shopping-Insight). 
This is an API-based application that gathers information such as, 
1. the most searched keywords for shopping categories, from one of South Korea's biggest IT company, NAVER.
2. other such as monthly searched numbers, product numbers, competition index, etc.

**⚙️ Languages and Packages Used**
- Language use: python
- Packages used: **`pandas`**, and more.

### Corporate Analysis
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

**⚙️ Frameworks and Packages Used**

**Financial Data Retrieval**
- `OpenDartReader` ***(API)***
- `FinanceDataReader`

**Data Analysis & Manipulation**
- `pandas`
- `numpy`

**Testing & Others**
- `pytest`
- `tqdm`
- `pickle`

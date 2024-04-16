---
title: "About"
layout: single
permalink: /about/
author_profile: true
sidebar_main: true
---
# Roger Kim

Hi! I am Roger Kim, a computer science student at Hanyang University located in Seoul, South Korea. With expertise in Python, C, C++, and C#, I am now working as a freelance web developmer, mainly using Django as my main framework. Additionally, I have a basic understanding of networking fundamentals and is proficient in various DevOps tools, such as Docker, AWS ECS, Git, and GitHub.

## My key skills
- Back-end development with ***django***
- Containerization with ***docker***
- Data Analysis&Manipulation with ***python***
- Deploying with various ***AWS*** tools(ECS, ECR, EC2, CloudWatch)
- Designing Software (Software Architecture)

## Projects
## Website - cmpnyinfo

This is a simple website that analyses the financial statements of corporations registered in Korean Composite Stock Price Indexes(KOSPI). It provides ***essential analytical data*** and ***visual representation*** using variouse types of graphs.

<!-- <p float="left">
  <img src="/assets/img/cmpnyinfo_final_home_page.png" width="44%" />
  <img src="/assets/img/cmpnyinfo_final_cmpny_page.png" width="44%" /> 
  <img src="/assets/img/cmpnyinfo_final_graph2.png" width="44%" /> 
  <img src="/assets/img/cmpnyinfo_final_graph.png" width="44%" /> 
</p> -->
<p float="left">
  <img src="/assets/img/cmpnyinfo_portfolio_detail_eng.png" width="45%" />
  <img src="/assets/img/cmpnyinfo_portfolio_main.png" width="44%" /> 
</p>

## OpenSource - NAVER Shopping Insight

A opensource project. Visit it [here](https://github.com/RogerKimJazzLover/NAVER_shopping_insight). 

This is an API-based application that gathers information such as, 
1. the most searched keywords for shopping categories, from one of South Korea's biggest IT company, NAVER.
2. other such as monthly searched numbers, product numbers, competition index, etc.

**⚙️ Languages or Frameworks Used**

Modules required are `pandas`, `request`, `time`, and more.

These are listed in `requirements.txt` in the `docs` folder. Use the below command to install these dependencies.

```pip install -r requirements.txt```

<p float="left">
  <img src="/assets/img/naver1.png" width="95%" />
  <img src="/assets/img/naver2.png" width="95%" />
</p>

## OpenSource - Corporate Analysis

A opensource project. Visit it [here](https://github.com/RogerKimJazzLover/PYTHON-Corporate-Data-Analysis).

This opensource, API-based project:
1. gathers & organizes the financial statements of companies listed in KOSPI(Korean Composite Stock Price Index); over the period of past six years.
2. calculates essential & meaningful ***analytical data***. For example:
    - ROA, ROE, PER, 
    - Revenue/Operating Income/Net Income increase rate
    - Profit Status
3. visualizes those datas in various types of graphs. (Box plot, scatter plot, etc)

**⚙️ Frameworks/Modules/Packages Used**

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

<p float="left">
  <img src="/assets/img/corporate_analysis1.png" width="95%" />
  <img src="/assets/img/corporate_analysis2.png" width="95%" />
</p>
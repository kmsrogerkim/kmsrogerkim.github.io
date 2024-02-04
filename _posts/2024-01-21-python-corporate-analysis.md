---
layout: single
title: "python: corporate analysis"
categories: python
tag: [python, pandas, data-analysis, data-manipulation]
---
## Subtitle: the core feature of cmpnyinfo

## Introduction

In this post, I am going to talk about the core feature of my website _"cmpnyinfo"_(visite [here](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-planning/) to checkout what my website's about).

The core feature of the website is basically in [this public Github repo](https://github.com/RogerKimJazzLover/PYTHON-Corporate-Data-Analysis). Here's what it does:
- Gather & organize the financial statements of 100 companies listed in KOSPI(Korean Composite Stock Price Index); over the period of ***past six years.***
- Calculate essential & meaningful ***analytical data*** for each company. Some examples of _essential analytical data_:
    - ROA, ROE, PER, 
    - Revenue/Operating Income/Net Income increase rate
    - Profit Status
- Visualize those datas in various types of graphs. (Box plot, scatter plot, etc)

## Workflow

![](/assets/img/python-corporate-analysis-workflow.png)

Here's a brief workflow of the code. There are three main python files that each has its own distinct purposes. _All of these files are ran by this one python file called **initialize_data.py**_. Here's a more detailed explanation of some of the main file.

**initialize_data.py**
- Runs all the files below using _subprocess_ package.
- So that we don't have to run all the file one by one.
- Instead, we can just run this one file.

**create_name_code.py**
- creates .pkl file using the _pickle_ python package.
- this _name_code.pkl_ file will be used across the python files in the repository; because the corporate code is needed when
    - calling the financial statement of the corporation using _OpenDartReader_
    - calling the stock data of the corporation using _FinancialDataReader_

**create_basic_info.py**
- creates a _basic_info.csv_ file.
- the _basic_info.csv_ file contains the following info about the 100 KOSPI companies.
    - Total Assets & Debt & Equity
    - Revenue & Operating/Net Income
    - Revenue & Operating/Net Increase Rate
    - Profit Status
    - ROA & ROE & EPS & PER
- All this info about each company, over the past six years.

**create_bf_for_analysis.py**
- creates a _basic_info_for_analysis.csv_ file based on the _basic_info.csv_ file.
- the _basic_info_for_analysis.csv_ file contains the following info about the 100 KOSPI companies.
    - Revenue & Operating/Net Increase Rate
    - Profit Status
    - ROA & ROE & EPS & PER
    - Current Stock & Future Stock


**If you want to see this data by yourself,** visit the _Data_ directory in [the Github repo](https://github.com/RogerKimJazzLover/PYTHON-Corporate-Data-Analysis/tree/master)

## Frameworks/Modules/Packages Used

**Financial Data Retrieval**
- `OpenDartReader` ***(API)***
- `FinanceDataReader`

**Data Analysis & Manipulation**
- `pandas`
- `numpy`
- `matplotlib`

**Testing & Others**
- `pytest`
- `tqdm`
- `pickle`
- more...

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
___
layout: post
title: "cmpnyinfo: the planning"
___


## Introduction

I am trying to make a website, where the users can search up a name of a company in the _KOSPI(Korean Composite Stock Price Index)_, and get the basic financial information of the company over the past decade or so.

Here's what I mean by 'financial information.'

1. Different types of incomes (Net Income, Operating Income, etc)

2. Ratios (ROA, ROE, PER, D/E, etc)

3. Others (market cap, stock prices, etc)

It is basically providing people a easy-to-access, easy-to-read financial statements of their company in interest, along with some essential analytical datas, ***ALL REPRESENTED IN GRAPHS***, so that you can effectively read the trend.

There are already websites like investing, but I want a more _light-weight, casual_ and perhaps maybe even mobile friendly website, _without all the pop up adds and advertisement videos playing in the corner._ 

**Key Values/Goals**

1. Light-weight

2. Casual

3. Simple

## General Structure (for now)

Whenever I have to build something in a level any bigger than a single, file, I draw out the general structure. Like this.

<img title="" src="file:///C:/Users/minse/OneDrive/문서/Blogs/1. cmpnyinfo. The planning/cmpnyinfo.drawio.png" alt="draw.io" width="770" data-align="inline">

Sorry for the unreadable texts. I use [draw.io](https://www.drawio.com/) to draw all my diagrams, I haven't found an effective way to share diagrams in draw.io.

***Tech Stack***:

- Git, Github

- Docker

- Python libraries (pandas, plotly, many more)

- DJANGO

- AWS ECS, EC2

- SQLite

## Challenges

To talk about a little bit about my self. I am _pretty new to building websites_. 

- ***AWS*** 
  
  - This will be my _first ever project to use AWS_. I have previouse experience with PaaS (render), but not IaaS. 

- ***Graphs***
  
  - Drawing graphs using the plotly library, and displaying onto the webpage, 
  
  - handling the graph between the API container and the Web-app container,
  
  - And all the other minor details. I can already see myself fixing a stupid bug for docker for hours 😭

# Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 

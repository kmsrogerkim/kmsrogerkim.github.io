---
layout: single
title: "cmpnyinfo: the UI"
categories: cmpnyinfo
---

## Introduction
In this post, I am going to talk about
- creating html&css templates in django for my website

## The File Structure
Before we dig in, I want to explain the file structure of my django project. My project consists of largely two seperate application.
- ***The UI***
    - Takes care of the html pages and user inputs
    - All the html pages are in the UI application,
- ***The API***
    - Uses _djangorestframework_ to get http requests from the UI application, 
    - then returns certain values, like yesterday's stock price of the given company and etc.

Here's a diagram to help you understand.
```
the root django dir
    - cmpnyinfo (project config for django)
    - static (images and css)
    - UI
        - templates
            - home.html
            - blach.html
            .
            .
            .
    - API
```

## The home.html
Here's how my home page looks like right now.

![](/assets/img/cmpnyinfo_home_page.png)
 
How does it look? Yeah I know. It's pretty bad. I was never good at designing anyways. 

So, while I am developing web-pages in django, I noticed some of it's unique features. Here's what I mean by ***django's unique features***
- handling static files (img&css etc)
- loading other html files (e.x: navbar)
- passing variables to the front-end
- csfr token

If you are interested in the things above, I wrote a post about it [here](https://rogerkimjazzlover.github.io/cmpnyinfo/django-template(html)-basics/)

Ok sure, ***other frameworks may also have these features***, but I never used them so I'm not sure.

## The cmpny.html
This page is for displaying the information of the company the user typed in the search bar.

![](/assets/img/cmpnyinfo_cmpny_page.png)

The page is not complete yet. The contents in the boxes will change. I am planning to include
- Different types of graphs, which will be placed in the third box, _seperated by tabs_.
- Summary of the company's financial statement (Operating income & etc) over the past few years.


***Usage of Language***

But there's a slight problem that's bothering me. THE LANGUAGE. The companies that the website support, are Korean corporations. Their names are in Korean. But everyting else is in English.

So I am planning to give each corporation an English name. I will try to look for a smart way to do it, but if I can't, I will probably just have to add all 100s of them one by one.

***Expected Issue***

Here's a veyr plossible scenario. The user enters _"samsung"_ in the search bar, but nothing shows up. Because _"samsung"_ is not listed in the Korean Composite Stock Price Index!(KOSPI). _"Samsung Electronics"_ is. It's like _"Google"_ and _"Alphabet Inc."_

I will have to look for ways to solve that issue, as well.

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
---
layout: single
title: "cmpnyinfo: status report"
categories: cmpnyinfo
tag: [ui, back-end]
---

## Introduction

On January 2nd, 2024, I uploaded my first post titled [cmpnyinfo: the planning](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-the-planning/). Since then, I have been working on this project and I would like to talk about the progress, and the current status of the project!

## UIs

### home 
![](/assets/img/status_report_home.png)

That is my home page. Not a lot changed from the beginning, but there were certainly a lot of improvements in terms of responsiveness. I put the instructions for using the website on top of the page. This is because when I visit a website, I just experience it, use it. I expect others to feel the same when trying out my website, so I put the "GET STARTED" div on top.

### Main page
<p float="left">
  <img src="/assets/img/status_report_cmpny.png" width="44%" />
  <img src="/assets/img/status_report_cmpny2.png" width="44%" /> 
</p>

That is my main page. The top box provides some basic stock information about the company. And for the _Summary of Financial Statement,_ you can scroll through it horizontally to view more information.

The graphs are seperated into three categories.

1. Box Plot
    - It show the average profit from trading the company's stock, based on the porfit status of the company. You can visit my website to experience it by yourself!

2. Numbers
    - It is a line graph illustrating the revenue, net income, total assets, total equity and all those numbers.

3. Ratios
    - It is also a line graph for all the ratios (Debt-Equity Ratio, ROA, ROE, PER, etc)

### About
![](/assets/img/status_report_about.png)

That is my about page. The first box provides some basic info about me. Then there's the ***list of all the companies my website is currently supporting***. The ***correct** names of each corporation is listed here, so if you are confused about the correct name of your company in interest, you can always search up their corporation code, or refer to this website.


## The Backend
![](/assets/img/status_report_backend.png)

Here is the general workflow for my website in a scenario where the user types the url _"/cmpnyinfo/005930"_ in the browser. _005930_ will be passed to the views as a string argument. Then the views return an html page accordingly.

I explained the backend part of my website in greater detail in these two posts. [_"cmpnyinfo: upgrading the API"_](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-upgrading-api/) & [_"cmpnyinfo: the API"_](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-the-api/).

This design has its disadvantages in terms of performance, since it is making an http request to the API everytime a user accesses an url. I am planning to solve this performance issue through ***caching***.

I am planning to cache the entire page, since the content of the page doesn't change at all throughout the day. For example, when the user requests for "x.x.x.x/cmpnyinfo/005930", I am going to cache that entire page and return it the next time it is requested.

If this method take up too much space in the memory, I could just cache the API responses from the API.

These methods will significantly increase the performance of my application.

## Conclusion

To sum up, I am done with the backbones of the website. The basic features are all working. ***All I have to do from now on is***

1. Containerize it
2. Deploy to AWS
3. Track & Improve performance
4. Improve UI&UX

## Written by

Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 



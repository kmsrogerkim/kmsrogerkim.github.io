---
layout: single
title: "Python: Developing with Python"
categories: python
tag: python
---

## Introduction
In this post, I wanted to share my experience of developing in python. When you're new to the language, it is hard to figure out how things are supposed to be done in general. So in this post, I will briefly talk about:

1. Why python is so popular
2. How to develop in python
3. How computers run python codes
    - Interpreter vs Compiler

## Why Python

We all know that python is a high-level, easy-to-read programming language. It is one of the most popular and used programming language in the world. The reason why it is so popular is, as you may have heard before, beacause it can be used ***anywhere.*** Now let me explain in more detail what it means.

### Libraries/Frameworks/Packages/Modules

So if you're completely new to developing/programming, you may not be familiar with the terms above. Those terms (Libraries/Frameworks/Packages/Modules) basically stands for: _collections of pre-written code that we use to do something._ ***These are the tools we use to actually build something.***

For example, if I want to 
1. **Build a website** in python
- Django, Flask

2. Do/Study/Research **Machine Learning** and/or **Data Science**
- Numpy, Pandas, 
- TensorFlow, PyTorch
- Matplotlib

3. Web Scraping/Crawling (Collecting data from the web)
- Scrapy, BeautifulSoup, Selenium

4. GUI - Tkinter

5. Many more...

## How Python

Ok, now you get it. Python can do all those things. But how? How do I install/download all those stuff? That's what ***pip*** or _Package Installer for Python_, is for.

You just have to create a virtualenv within the terminal's python environment using packages like venv(python's built in package). Then
```
pip install name_of_package/framework/whatever
```
Now if you're wondering what and why create virtualenv, take a look at [this post](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-first-step/)

So for example, if I want to make an website with python, so I decided to use a web framework called _django,_ all I have to do (primarily of course), is 
```
pip install django
```
It's very simple and straightforward (for most of the time, at least). Especially when you're developing in Linux.

Ok now you installed all the tools you need. ***But where should I write my code?***

If you are into Machine Learning or Data Science, Jupyter Notebook is probably what you should use. It is basically a web application that allows you to look at the data you are manipulating, as you code. It looks something like this.
![](/assets/img/jupyter_notebook.png)

Most other things, web development, web sraping, tkinter(GUI), are done in text-editors, IDEs, and terminal. You basically write a _.py_ file, and the python interpreter does its magic. Speaking of python interpreter...

## How Computer Runs Python Codes

research - pythonics codes , interpreter vs compilter, https://kmahireddy123123.medium.com/explain-about-python-interpreter-and-compiler-b2ffd3084826

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
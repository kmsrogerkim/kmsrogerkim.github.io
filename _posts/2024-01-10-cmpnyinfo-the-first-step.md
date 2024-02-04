---
layout: single
title: "cmpnyinfo: the first step"
categories: cmpnyinfo
tag: [python, dependency-management, virtualenv, django, db, dbms]
---

## Introduction

Now it's time to start building the website. In this page, I am going to talk about:
- Setting up an developing environment for django in WSL
- A little bit about managing dependencies in python (virtualenv, pyproject.toml)
- Setting up an environment for my django project (DBMS, future scalabilty issues.)

If you want to know about the general planning stage, and the structure of the website, visit my [Previous Blogs](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-planning/)

## Setting Up an Isolated Environment

I am currently developing in WSL2, with Ubuntu distro, in Windows 11. Developing in WSL has its pros and cons, which I might discuss in another post, but the experience havn't been too bad for me.

I created a python virtual environment using the _virtualenv_ and _virtualenvwrapper_ package. The detailed steps are describe in [this stackoverflow page](https://stackoverflow.com/questions/12232421/virtualenvwrapper-commands-arent-working)

## Why use virtualenv: short discussion about version control in python
The _virtualenv_ package is one of many ways to manage dependencies for your python applications/projects. I am using the _virtualenv_ and _virtualenvwrapper_ packages, which was considered the standard way until few years ago, I think; (I don't know I'm just a student). 

It allows you to:
- create ***isolated developing environments*** for different python projects, which ensures that each project has its own set of dependencies
- create a ***portable*** environment that can be easily replicated on different machines

But python ***now have their own built in _venv_ module*** for python3. Meanwhile, _virtualenv_ is a _package_ you download through _pip._ I mean, I have to admit that now in 2024, ***virtualenv is sort of outdated***.

***Then why am I still using virtualenv?*** Well it's because
- First, it is working. The most basic principle of programming states that: ***"If it's working, don't touch it."***
- Second, it is straightforward.
- Third, it saves you trouble when using with _virtualenvwrapper_ package. With this package, you don't have to worry about _.venv_ folders. It just straightforwad-ly makes you an isolated environment.


I use it basically to create a clean _requirements.txt_ for my project, and it's working just fine, so I'm happy with it. And I believe it is still the standard action to take when you're just making a small application, or a small open-source project on Github.

**BUT,** there are some alternatives to manage your dependencies, rather than just a _requirements.txt_ file. In fact, if you are managing a larger scale application/project, and you are serious about managing dependencies, ***you will need more than just a requirements.txt file.*** 

Back in the days (which I am not familiar with), ***setup.py*** file was the go-to method. But now, ***pyproject.toml*** file with ***poetry*** is the standard way for _professional project and dependency management_.

For my website, I'm just going to stick with _requirements.txt_ file. But I am planning to ***study more about professional project and dependency management*** in near future.

## Setting Up the Django Project

Install _django_, and for my case, _djangorestframework_ as well, since one of my apps is going to be an API module, as I discussed in [cmpnyinfo: the architecture](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-architecture/).

I am not going through the detailed commands and modification of files such as _urls.py_ and etc. There are plenty of detailed tutorials for that in YouTube. But it is worth to mention about my choice of DB.

### Choosing DB/DBMS for my website
I used render(a PaaS) to deploy my first django website. And the way I managed DB in that project is that,
- Run a PostgresSQL server, get the External Database URL
- Then set that URL as the database setting in the django's _settings.py_ using environmental variable, like this
```
DATABASES = {
    'default':dj_database_url.parse(os.environ.get("DATABASE_URL"))
}
```
This way, you can easily deploy your website, and the readers can write to the DB, and read from it, all the time. **HOWEVER**, ***I don't really need that for this website***. The DB will stay _static_ most of the time. So I am thinking about using sqlite3 as my DBMS.

 Let me explain what I mean by my website will ***stay static*** most of the time. 
 
 ![](/assets/img/cmpnyinfo_architecture.png)

As you can clearly see from the diagram. The user will ***never write to the DB***. In fact, it will ***barely need to be updated***. The csv tables will be stored as _.csv files,_ perhaps in S3. All the DB is going to store, is the list of companies supported, and a text field for some basic information about the company.

***In the future,*** I might need to use PostgresSQL for these two possible scenarioes
1. Traffic grows so that the web-app cannot simultaneously read from the local sqlite3 db
2. I want to implement user-authentification

The possibility of the first scenario happening is very low for these reasons
1. I will not advertise/promote my website (I'm broke and this is just a student's project)
2. The data the web-app needs to read from the DB is very small and will be done in an instance, so I predict that it would take a lot of traffic to break it.

The second scenario is likely to happen. Since I want to allow people to kind of _star_ the companies they're interested in, and this process would require me to add a table for list of users in my DB. The web-app needs to update the DB whenever there's a user tries to sign up, and reads from it whenever the user sings in, or check the list of their _stared_ companies. For this, I have several options.

***Option 1. Keep using sqlite3***

Well, if I know that nobody is going to visit my website, I wouldn't have to worry about it. And even if there are _some_ traffic, I think the system will hold.

**BUT WHAT IF?** What if I want to expand my website? If there are already sensitive data of some users in the local sqlite3 DB, like their passwords and e-mail, will I be able to migrate that to PostgresSQL? That's a question I don't have an answer to right now.

***Option 2. Use PostgreSQL***

Ok then, just use PostgresSQL, or other proper-DBMS. Problem solved.

**BUT REALLY?** I don't want to add extra layer of complexity for some feature I _might_ implement in future. 

**IS IT NECESSARY?**
Economically speaking, if this feature requires some investment (the fee to run the server for the DB), but is not predicted to bring the company (me) back more money than the investment, then the feature should not be deployed.

***My solution***

The solution is quite simple. Just deploy the website with sqlite3, then wait to see if the website is going to grow. If it grows, and you want to add that extra feature, then go ahead and deploy another server for the DB, or find some way other than local DBs.

## Conclusion
So in conclusion,
- I generated an isolated environment for dependency management using _virtualenv&virtualenvwrapper_
- I generated the django project and apps inside the project, and modified it's configurations accordingly.
- I am going to use sqlite3 and local DBs initially, but might migrate to other services, and deploy server for the DB.

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
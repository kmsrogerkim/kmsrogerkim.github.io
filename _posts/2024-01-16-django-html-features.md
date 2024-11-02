---
layout: single
title: "django: html features"
categories: django
tag: [html-css, django, front-end]
---

## Introduction

In this post, I am going to talk about
- the "include" feature in django (nabvar)
- static files in django
- csrf token

## Creating a navbar in django (include feature)

On top of every html page in my wbesite, there's a code to include my navbar into the webpage. Like this,

[//]: # {% raw %}
```
{%include "navbar.html"%}
```
[//]: # {% endraw %}

This "navbar.html" is a seperate html file that I made for my website's navbar. This feature really does come in handy because it allows you to easily reuse your html files, from another html file; just like my navbar!

## CSS (static files) in django

Django also has its unique way of managing static files. In order to use static files (css, js, images) in django, you have to

1. Create a directory called "static" in your project's root directory
2. Inside the "static" directory, create another directory with the name of the app you want to store the static files in.
    - For example, the css, js and image files for a django application called "ui", should be stored in the "projct_root/static/ui/"
3. Go to the _settings.py_ file for your project, then 
```
    STATICFILES_DIRS = [
	    os.path.join(BASE_DIR, 'static'), #remember to include the 'os' package
    ]
```

Now, when you want to refer to those css files in your html,

[//]: # {% raw %}
```
{%load static%} #Do this
<!DOCTYPE html>
...
    <link rel="stylesheet" href="{%static 'ui/name.css'%} #and something like this
...
```
[//]: # {% endraw %}
## CSRF Token

In django, whenever you want to accept an user input, or in other words, allow the user to ***post*** to your server, you have to include

[//]: # {% raw %}
```
<form method="POST>
    {%csrf token%} #this thing right here
    some other code ...
<form>
``` 
[//]: # {% endraw %}

That _"csrf token"_ is a token that django uses to prevent CSRF (Cross Site Request Forgery). CSRF is a type of security vulnerability that tricks a victim into executing an unwanted action on a web application in which they're authenticated.

1. Django generates a csrf token, each token unique for each sesssion
2. Then stores in the session data
3. It is also set in the csrftoken cookie that's sent to the user's browser
4. Now, whenever you make a POST request, django checks on the token to see if the request is valid(not including any un-wanted changes that you didn't put in the form).

## Contact Me:

Roger Kim

[Github](https://github.com/kmsrogerkim)

e-mail: <minseungkim1017@gmail.com> 

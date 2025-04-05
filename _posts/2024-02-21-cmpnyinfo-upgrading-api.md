---
layout: single
title: "cmpnyinfo: upgrading the API"
categories: cmpnyinfo
tag: [rest-api, back-end]
---

## Subtitle: learning from mistake

## Introduction

While writing [this post](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-designing-rest-api/), I realized that my REST APIs were unnecessarily accepting POST requests. Since my API requests focuses on retrieving/reading data about the given company, I really think that it should only recieve GET requests.

I believe this is one of the reasons why one should journal while working on a project; to reflect on oneself and spot mistakes. While writing these posts, I was able to fully organize my mind, and really just view this entire project/code/infrastructure/design/architecture from a third person's view. So I recommend you to do it as well!

In this post, I'm going to talk about how to

1. pass data/arguments through url in django

## urls.py - API

In the _urls.py_ file in the API section of the project, I set the url patterns as follows.

```
from django.urls import path
from . import views

urlpatterns = [
	path("basicInfo/<str:cmpnyData>", views.get_basic_info),
    .
    .
]
```
Now, whatever that comes after the "basicInfo/" in the url, ***will be passed into the views.get_basic_info function as an argument, as a string.***

## views.get_basic_info - API
```
@api_view(['GET'])
def get_basic_info(request, cmpnyData: str):
    cmpnyname = initialize_cmpnyname(cmpnyData)
    if not cmpnyname: #If the cmpny is not in the list (404)
        return Response({"error": "NOT FOUND: cmpnyname not in list"}, status=status.HTTP_404_NOT_FOUND)
    .
    . #some more code
    .

    return Response(basic_info)
```
You can see how there is an extra parameter called _cmpnyData_ to the function ```get_basic_info```. That is the parameter ***that recieves*** what's passed into the function as an argument through the url.

The ```initialize_cmpnyname()``` function will basically return _None_ if the cmpnyname/corp_code is not supported(doesn't exist in the dictionary), or return the cmpnyname if the corp_code is passed in as an argument.

### For example
**005930 -> 삼성전자(Samsung Electroncis)**

## Calling the API - UI

Now, in the views.py file in the UI app, we can just make a GET request.
```
#BEFORE
basic_info = requests.post("http://localhost:8000/api/basicInfo/", data={"cmpnyname":cmpnyname})

#AFTER
basic_info = requests.get(f"http://localhost:8000/api/basicInfo/{cmpnyname}")
```

## Result

As a result, I achieved a

1. Cleaner code
2. Straight forward API design; making it intuitive and easy to use
3. Better security; since it doesn't recieve POST requests

## Contact Me:

Roger Kim

[Github](https://github.com/kmsrogerkim)


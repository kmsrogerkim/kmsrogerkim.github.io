---
layout: single
title: "cmpnyinfo: the API"
categories: cmpnyinfo
tag: [django, rest-api, back-end]
---

## Introduction

In this post, I am going to talk about
- Setting up the "API" app with djangorestframework
- Communicating between the "UI" app and the "API" app

In the [previous post](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-the-ui/), I talked about setting up the UI app for my project. In this post, I will be talking about setting up the "API" application inside django, which will serve as an REST API. Additionally, I am going to write down some commands and codes that is required for building a REST app in django.

## Setting up the "API" app

```
pip install djangorestframework
```
In your root directory for the django project
```
python3 manage.py startapp API#the name of the app
```

Then go to the _settings.py_ file for the project, and add the following line inside the _INSTALLED_APPS_ array.
```
'rest_framework',
```
Don't forget to make an _urls.py_ file inside your newly formed django app directory. Then add your new url path to the _urls.py_ file ***in the root project directory.*** Like this,
```
urlpatterns = [
    path("admin/", admin.site.urls),
    path("", include("other_app.urls")),
    path("api/", include("api_app_name.urls")),
]
```
Then, you should include these two packages in your app's _views.py_ file. My _views.py_ file looks sth like this:
```
from rest_framework.response import Response
from rest_framework.decorators import api_view


@api_view(['GET'])
def get_cmpnyname(request):
    cmpnyname = {"cmpnyname":"whatever"}
    return Response(cmpnyname)
```

## Communication between UI and API

Now that we've got the API set up (of course that's not all the codes, the functions in the views.py actually does something). We just have to make an request to that API app from the UI app. And here's how I did it.

First, I modified the _ALLOWED_HOSTS_ setting in the _settings.py_ for the porject, to this.
```
ALLOWED_HOSTS = ['localhost', 'some_other_stuffs_perhaps...']
```
This allows our API app to handle http requests sent by the UI app. Like this
```
#In the views.py file in the UI app
def view_balch(request):
	cmpnyname = requests.get("http://localhost:8000/api/corresponding-url-for-api")
```
As you can see, the apps are communicating through http requests, and the API app is doing its job as an API service! It may not be the best way to communicate, or share data between apps in django. However, this is a special case since I specifically designed it to be this way (You can refere to [this post](https://kmsrogerkim.github.io/cmpnyinfo/cmpnyinfo-the-architecture/)). So that I can have these advantages:
- Easy to seperate the API side of the website into a microservice
    - which makes the API ***reusable*** in the future
- Easily scale the API side of the web in the future
- Isolate the data that is needed for corporate analysis, from the UI's data (perhaps sensitive user-info in the future).

## Conclusion

In conclusion, I 
- created a new app in django for the API part of the website
- installed additional dependencies in order to set up a REST API application
- modified settings and url paths
- managed communication between the UI app and the API app

## Written by

Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 


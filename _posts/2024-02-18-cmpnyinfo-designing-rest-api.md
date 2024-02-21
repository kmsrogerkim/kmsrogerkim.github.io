---
layout: single
title: "cmpnyinfo: designing REST API"
categories: cmpnyinfo
tag: [api, rest-api, back-end]
---

## Introduction

_“Application Programming Interface,” or API, refers to a communication channel between various software services_[[1]](https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428).

In this post, I am going to talk about 
1. _How to design REST API_
2. _Some examples from my project, [cmpnyinfo](https://rogerkimjazzlover.github.io/cmpnyinfo/cmpnyinfo-the-api/)_.

## What is REST?

REST stands for _representational state transfer_. It is an architectural style that uses _stateless client-server communication, meaning no client information is stored between get requests and each request is separate and unconnected_[[2]](https://www.redhat.com/en/topics/api/what-is-a-rest-api). It uses URIs to identify resources and applies HTTP methods for CRUD operations on these resources.

## Good Practices

### 1. Use nouns for endpoint paths, not verbs.

For example, here's a code from my project
```
def cmpny(request, cmpnyname):
	basic_info = requests.post("http://localhost:8000/api/basicInfo", data={"cmpnyname":cmpnyname})
```

The server is sending a http POST request to the URI of ```/api/basicInfo```, with the name of the company, (cmpnyname) as POST data

### 2. Don't use _

When you desing the uris, don't design them like ```api/basic_info```. Instead, design them using (-), or capital letters, like ```api/basic-info``` or ```api/basicInfo```

### 3. Use plurals

```/employee/:id/``` -> ```/employees/:id/```

### 4. Use proper status codes

Here are some examples of commonly used status codes and their meaning

![](/assets/img/status_codes.png)

This way, it is easier to handle exceptions and errors, since you can identify what went wrong. Here's an example code from my project.

In the API side, I am going to return a 404 NOT FOUND status code when the company is not one of the keys in the ```name_code``` dictionary; meaning that our website doesn't provide any information regarding that company.
```
from rest_framework import status
@api_view(['POST'])
def get_basic_info(request):
    try:
        cmpnycode = name_code[cmpnyname]
    except KeyError:
        return Response({"error": "Bad Request: cmpnyname not in list"},    
        status=status.HTTP_404_NOT_FOUND)
```

Here's a documentation for all the status codes in djangorestframework. [Click Here](https://www.django-rest-framework.org/api-guide/status-codes/) or copy-paste this url

https://www.django-rest-framework.org/api-guide/status-codes/

Then, in the client's side, I can handle the errors. If I don't handle the errors like this, every error would return 500 internal server error, making it impossible to identify the problem

```
#Calling API
basic_info = requests.post(api uri, post data)
finstate_sum = requests.post(api uri, post data)
graph_data = requests.post(api uri, post data)

if basic_info.status_code != 200 or finstate_sum.status_code != 200 orgraph_data.status_code != 200:
    return redirect("error_page")
```

### 5. Don't return plain text

_REST APIs should accept JSON for request payload and respond with JSON because it is a standard for transferring data_[[1]](https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428).

The response should not only be formatted in JSON, but the content-type in the response header should be set as application/JSON.

I only have to make sure that the response is properly formatted as JSON since the ```Response``` module would set the header accordingly.

Import like this
```
from rest_framework.response import Response
```
Use like this
```
    return Response(dictionary_object_here)
```

### 6. Security

1. _always use SSL/TLS, with no exceptions_[[1]](https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428)
2. _allow authentication via API keys, which should be passed using a custom HTTP header with an expiration date_[[1]](https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428)

### 7. Versioning

Our future APIs should not affect the current users using our API. Different users use different versions and we should seperate them and support them. _API versions can be passed through HTTP headers or query/path params._[[1]](https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428) For example, ```/products/v1/4```

### 8. Documenting

Of course, you have to document what your API provides and how others can use it.

## References.

This post contains a lot of quotes from this great post from medium, written by Dr. Milan  Milanovic.

_1. https://medium.com/@techworldwithmilan/rest-api-design-best-practices-2eb5e749d428_

And a quote from this website.

_2. https://www.redhat.com/en/topics/api/what-is-a-rest-api_

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
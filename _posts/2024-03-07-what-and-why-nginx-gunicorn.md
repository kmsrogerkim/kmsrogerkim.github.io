---
layout: single
title: "What and Why: Nginx, Gunicorn"
categories: django
tag: [back-end, django, software-architecture, nginx, wsgi, web-server]
---

### Subtitle: let's deploy django

## Introduction

In this post, I am going to explain
1. What nginx and gunicorn is
2. Why we need them

## What is NGINX?

Nginx is mainly a web server. But it is also a reverse proxy server, a load balancer, and many more. Let's say that you have just finished building your django project, and have successfully ran it in your local computer with a command like `python manage.py runserver`; that's a web-application you just have created. Now we have to deploy that web-application with a web server, such as nginx!

## Why do we need NGINX?

Now you may wonder why you need such thing as a webserver. Why can't we just run `python manage.py runserver` on our physical servers(e.x: EC2 instance)?

### 1. Static Files

Nginx handles static file such as .js, .css and image files for you. Yes, django's server can handle static files. However, nginx handles them much faster and more efficient than django's server. This way, the django server can focus more on implementing business and application logic.

### 2. Caching

Nginx has built-in caching capabilities that can be utilized to cache responses from your django application. This will increase the overall performance of your website, and therefore providing a better experience for your users.

### 3. Security

Nginx allows you to add an extra layer of protection, which I believe is necessary when it comes to deploying your django app to the real world. For example,
1. **Rate limiting** - it can limit the rate of requests from a certain IP addresses, which is essential when it comes to preventing DDoS attacks.
2. **Reqeust filtering** - you can allow only a certain types of requests into your web-application. For example, if you don't want your django application to handle any POST requests, nginx allows you to filter POST requests before it reaches django, adding an extra layer of security.
3. **SSL/TLS Termination** - SSL and TLS credentials are the ones that make your url from `http://` to `https://`. There's a complex encryption and decryption process involved in secure https requests. Which again, nginx can handle for you so that the django server doesn't have to.
4. **Port Security** - Assuming that your django app is running or port 8000, or 8080, I wouldn't recommend you to leave those ports wide open to the outside world! You can set the configurations so that only nginx running with local IP address can access your application; adding an extra layer of security to your application. This is also where the **reverse proxy** feature of nginx comes in.

### 4. Reverse Proxy

Let's say the user types `http://your-url.com` into the browser. Since it's `http` and not `https`, the request will go through the port 80. But your django application is running on port 8000! That's when nginx comes in. Nginx will listen on port 80, or 443 for requests. When a request comes in, nginx will validate it according to your configuration like how I mentioned above (checking the request type, etc), then, if everything checks out, it will pass the request to your django application running on port 8000.

### 5. Load Balancing

Let's say you have more than one django application running, or you may have more than one instance of the same application. Then you need a load balancer to distribute the incoming requests to the different instance/applications. And yes, nginx also provide you with the load balancing feature!

## What is GUNICORN?

Ok, now you get what nginx is and why need it. Then what is gunicorn?

Well gunicorn is a wsgi. WSGI, or Web Server Gateway Interface is an interface between the web server and the web-application. When a web server, like nginx, forwards the requests from the outside world to the web application, it cannot directly reach out to the application layer. The WSGI handles the requests and runs the Server Side applications.

![](/assets/img/nginx-gunicorn-workflow.png)

## Why do we need WSGI?

Yes, you can run `python manage.py runserver` to run a django server that listens on port 8000. But then it will have some unnecessary features, like handling static file, and it would be slow and inefficient.

Since now you are going to run nginx, which will handle static files for you, you don't need your django app to handle them! Also, WSGIs, like gunicorn, is much more ***lightweight***, ***efficient***, ***fast*** and ***secure*** than the django's own server.

## Conclusion

1. Nginx is an extremely efficient and fast web server, reverse proxy server, load balancer, and many more. It provides a lot of features, like load balancing, request filtering, static file handling and many more. It is essential in order to improve the performance of your web-app.
2. Gunicron is a WSGI(Web Server Gateway Interface), that acts as an interface between the web server, and the web application.

## Written by

Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 


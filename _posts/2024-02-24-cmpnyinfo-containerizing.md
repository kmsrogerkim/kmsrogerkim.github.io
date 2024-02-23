---
layout: single
title: "cmpnyinfo: containerizing"
categories: cmpnyinfo
tag: [docker, containerization]
---

## Introduction

In this post, I am going to talk about

1. What docker & container are
2. How to write dockerfile for my django application
3. Basic docker commands
4. Uploading docker image to the Dockerhub

## What is a container?

Containers are a running process of application that is built based on an image, which are bundles of  packages that allows applications to run on multiple devices with great portability. Containers are isolated, up to a certain degree, from each other, and the host's machine.

So basically, you build an image, which is a blueprint for building your application. The image includes something like...

1. The files it needs (source codes, configuration files)
2. Configurations (e.x: Where they should be (working directory, etc))
3. The dependencies (frameworks, libraries, etc)
4. some more depending on your application

Then, you let the container engine, such as docker, to run that image. That application that's running, which was built based on the image, is a container.

## Building the image - Dockerfile

So I made this web application on my computer. Now I can just build an image of it, so that I can run my application on a real server. Now how can I do that? Through dokcer!

I am not going to talk about how to install docker on your machine. But I am going to share how I built my image for my django project using Dockerfile.

First, create a file exactly named `Dockerfile` in the root directory of your project.

### Dockerfile

Dockerfile is basically a set of instructions that tells docker how to build your image. Here, let me explain with the Dockerfile I wrote for my project.
```
FROM python:3.10

WORKDIR /usr/src/app

ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONUNBUFFERED=1

COPY . /usr/src/app/
RUN pip install -r requirements.txt

EXPOSE 8000

CMD [ "python", "manage.py", "runserver","0.0.0.0:8000"]
```
1. ```FROM python:3.10```
    - Tells that this image(django app), is built upon another image, which is python 3.10.
2. ```WORKDIR /usr/src/app```
    - Tells where the application should be
3. ```ENV PYTHONDONTWRITEBYTECODE=1```
    - This environment variable prevents Python from writing .pyc or .pyo files on the disk. In a docker container, these files can take up unnecessary space, so it's common to set PYTHONDONTWRITEBYTECODE to prevent them from being created.
4. ```ENV PYTHONUNBUFFERED=1```
    - By default, python collects several outputs in a buffer before writing them all at once to the terminal. In a Docker container, this can cause the output to be delayed, which can be problematic when you're trying to observe the behavior in real time. ```PYTHONUNBUFFERED=1``` disables this buffering.
5. ```COPY . /usr/src/app/```
    - ```COPY``` -> Copy
    - ```.``` -> what's here in host machine
    - ```/usr/src/app/``` -> To here on image/container
6. ```RUN``` -> run this command (in container)
7. ```EXPOSE 8000``` -> listen for outside requests in this port
8. ```CMD```
    - Acts as an entrypoint linux command. Meaning that it serves as the starting point for a Docker container's runtime process
    - Always in Dockerfile. Always at the end of the file.

### Some warnings

This image might work just fine. But it is certainly not the best one. Especially the ```COPY . /usr/src/app/``` line. It is important to not have any sensitive files inside your image (e.x: API keys, secret keys). And it is always good to keep your image as clean and minimal as possible.

## Basic docker commands

So after you write that Dockerfile, run the `docker build -t name:tag .`

Below are some useful and commonly used docker commands

1. `docker ps` -> tells what containers are running
2. `docker container ls -a` -> view every container, even the ones that’s not running
4. `docker run the_image_id` -> runs a container based on the image
5. `docker start container_id` -> starts the existing container
6. `docker rename old_container_name new_container_name`
7. `docker rm container_id`
8. `docker rmi image_id:tag`
9. `docker exec -it container_id bash`  Allow you to enter the terminal in a running terminal
10. `docker logs container_id` view logs

## Dockerhub

It is basically a place where you upload your images to.

1. `docker login`
    1. e.x: `docker login -u username -p password`
2. `docker tag local-image:tagname username/repo:tagname`
    1. giving the already existing image a tag for remote repo (Dockerhub)
    2. getting ready to push
3. `docker push username/repo:tagname`

To pull an image from the hub,

4. `docker pull username/repo-name:1`

## Conclusion

So in this post, I explained 
1. What docker & container are
1. Basic docker commands
1. How I wrote dockerfile for my django application
1. How I uploaded docker image to the Dockerhub

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 

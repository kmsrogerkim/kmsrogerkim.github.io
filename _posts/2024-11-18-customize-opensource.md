---
layout: single
title: "Customize DRF Simplejwt"
categories: python
tag: [python, drf, opensource] 
---
## Introduction 
In this post, I am going to talk about how I customized the code from the [drf-simplejwt repository](https://github.com/jazzband/djangorestframework-simplejwt) to build a custom authentification flow for my [toyki project](https://toyki-homepage.vercel.app/). It is a **very simple** customization, and some may consider it uneccessary. However, there was a specific need for a custom workflow with jwt tokens from the front-end developer, which I will talk about in detail in the Background section. Also, I believer it was a good chance to dip my toe into the pool of opensource code and playing with them.

## Background
The project required a custom workflow to determine whether the refresh token and the authentification token were valid or not. The front would pass the access token and the refresh token all together to the `api/token/valid` endpoint. Then I would have to determince if the access token and the refresh token are valid or not. The problem was that, when the access token was passed through the header directly without the bearer prefix, a CORS error would occur. However, when the access token is passed through the header with the bearer header, the default JWTAuthentication workflow from the simplejwt would immediately return 401, regardless of the validity of the refresh token. So I decided to set up a simple authentication class based on the JWTAuthentication class in the simplejwt, that checks for both the access and refresh tokens' validity.

## Original Code
First of all, I would want to find out which code from the simplejwt takes care of the authentication process. This can be done my reading the documentation, or in my case, checking for the DEFAULT_AUTHENTICATION_CLASSES tuple in the settings.py. You can see from the code below, it is set to the JWTAuthentication class from the authentication file in the rest_framework_simplejwt package.
```
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        `rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}
```
Now let's go to github and checkout how that JWTAuthentication class looks like. You can checkout the full code in [jazzband's repo](https://github.com/jazzband/djangorestframework-simplejwt/blob/master/rest_framework_simplejwt/authentication.py), the key codes are below
```
```

## Contact Me:
Roger Kim

[Github](https://github.com/kmsrogerkim)

e-mail: <minseungkim1017@gmail.com> 


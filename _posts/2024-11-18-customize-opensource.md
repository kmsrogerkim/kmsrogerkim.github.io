---
layout: single
title: "Customize DRF Simplejwt"
categories: python
tag: [python, drf, opensource] 
---
## Introduction 
In this post, I am going to talk about how I customized a part of the [drf-simplejwt repository](https://github.com/jazzband/djangorestframework-simplejwt) to build a custom authentification flow for my [toyki project](https://toyki-homepage.vercel.app/). It is a **very simple** customization. There was a specific need for a custom workflow with jwt tokens from front-end, which I will talk about in detail later.

## Background
The project required a custom workflow to determine whether a pair of refresh and access token were valid or not. Client would pass the tokens all together to the `api/token/valid` endpoint. Then the server would have to determince if the access and the refresh token are valid or not. The problem was that when the access token was passed through the header directly, without the bearer prefix, CORS error would occur. However, when the access token is passed through the header ***with*** the bearer header, the default JWTAuthentication method provided by the simplejwt would immediately return 401 when the access token is invalid, regardless of the validity of the refresh token, and the permission class of the view. So I decided to set up a simple custom authentication class based on the JWTAuthentication class in the simplejwt, that checks for both the access and refresh tokens' validity.

## Original Code
First of all, I searched for the code for JWTAuthentication from the simplejwt repo. If you check the DEFAULT_AUTHENTICATION_CLASSES tuple in `settings.py` it is probably set to the JWTAuthentication class, which, if you recall, was configured by you when you added the simplejwt to your service.
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'rest_framework_simplejwt.authentication.JWTAuthentication',
    )
}
```
Now let's go to github and checkout the code. You can checkout the full code in [jazzband's repo](https://github.com/jazzband/djangorestframework-simplejwt/blob/master/rest_framework_simplejwt/authentication.py). The key codes are below.
```python
class JWTAuthentication(authentication.BaseAuthentication):
    """
    An authentication plugin that authenticates requests through a JSON web
    token provided in a request header.
    """
    ...
    def authenticate(self, request: Request) -> Optional[Tuple[AuthUser, Token]]:
        header = self.get_header(request)
        if header is None:
            return None

        raw_token = self.get_raw_token(header)
        if raw_token is None:
            return None

        validated_token = self.get_validated_token(raw_token)

        return self.get_user(validated_token), validated_token
    ...
    def get_validated_token(self, raw_token: bytes) -> Token:
        """
        Validates an encoded JSON web token and returns a validated token
        wrapper object.
        """
        messages = []
        for AuthToken in api_settings.AUTH_TOKEN_CLASSES:
            try:
                return AuthToken(raw_token)
            except TokenError as e:
                messages.append(
                    {
                        "token_class": AuthToken.__name__,
                        "token_type": AuthToken.token_type,
                        "message": e.args[0],
                    }
                )

        raise InvalidToken(
            {
                "detail": _("Given token not valid for any token type"),
                "messages": messages,
            }
        )
```

## Customizing
So I created some custom exceptions first. When you look at the original code, you can see the `InvalidToken` exception which is in the [exceptions.py file](https://github.com/jazzband/djangorestframework-simplejwt/blob/master/rest_framework_simplejwt/exceptions.py). I created a `custom_exceptions` file which looks like this.
```python
from rest_framework_simplejwt.exceptions import AuthenticationFailed
from django.utils.translation import gettext_lazy as _

class InvalidAccessToken(AuthenticationFailed):
    status_code = status.HTTP_400_BAD_REQUEST
    default_detail = _("Access token is invalid or expired. Please refresh using refresh token")
    default_code = "Invalid access token"

class InvalidRefreshToken(AuthenticationFailed):
    status_code = status.HTTP_400_BAD_REQUEST
    default_detail = _("Refresh token is invalid or expired")
    default_code = "Invalid refresh token"
```
This codes looks simple, and is simple. It just inherits the `AuthenticationsFailed` class from the simplejwt, and creates two new exceptions, Invalid `access` token, invalid `refresh` token, Before, the simplejwt would just return InvalidToken error, but now, we can specify which token is invalid.

Then, I created a new custom authentication file that looks something like this.
```python
# import neccessary packages, including the JWTAuthentication base class
from api.custom_rfs_exceptions import InvalidAccessToken, InvalidTokens, InvalidRefreshToken

User = get_user_model()

class CustomJWTAuthentication(JWTAuthentication):
    # function to be overrided
    def get_validated_token(self, raw_token: bytes, **refresh_token):
        """
        Validates an encoded JSON web token and returns a validated token
        wrapper object.
        """
        refresh_valid = False
        access_valid = False
        messages = []

        # this is where it gets different from the original code.
        # this loops makes sure to check for both the refresh and the
        # access token, and return the correct exception
        for AuthToken in api_settings.AUTH_TOKEN_CLASSES:
            if refresh_token['refresh_token'] is not None:
                refresh_token = refresh_token['refresh_token']
                try:
                    refresh = RefreshToken(refresh_token)
                    refresh_valid = True
                except (InvalidToken, TokenError):
                    pass
                try:
                    access = AuthToken(raw_token)
                    access_valid = True
                except (InvalidToken, TokenError):
                    pass

                if refresh_valid and access_valid:
                    return access
                elif refresh_valid and not access_valid:
                    raise InvalidAccessToken()
                elif not refresh_valid and access_valid:
                    raise InvalidRefreshToken()
                raise InvalidTokens()

            try:
                return AuthToken(raw_token)
            except TokenError as e:                
                messages.append(
                    {
                        "token_class": AuthToken.__name__,
                        "token_type": AuthToken.token_type,
                        "message": e.args[0],
                    }
                )

        raise InvalidToken(
            {
                "detail": _("Given token not valid for any token type"),
                "messages": messages,
            }
        )
```
This code is really simple too. Just some additional if statements to check for both the access and the refresh token. You can check out the `AUTH_TOKEN_CLASSES` settings in the settings document for the simplejwt. Here's the default tuple
```python
"AUTH_TOKEN_CLASSES": ("rest_framework_simplejwt.tokens.AccessToken",),
```

Now in the settings, just have to change the default authentication classes to that file I created in the app called my_app.
```python
REST_FRAMEWORK = {
    'DEFAULT_AUTHENTICATION_CLASSES': (
        'my_app.authentication.CustomJWTAuthentication',
    )
}
```

## Conclusion
The customization is fairly simple. But it was really a great to customize, read and play with opensource code. I finally got to realize what `opensource` really meant, how it works, and how to customize them. I also realized that it is very fatal to read the documents, and I spent quite a time reading the opensource code just to understand how it works. I am looking forward to customize more opensource codes in the future, and one day, maybe even contribute to one.

## Written by
Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 




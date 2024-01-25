---
layout: single
title: "Jekyll Liquid Syntax Error"
categories: bugs
tag: [jekyll, bug-fix]
---

## Introduction

When I was writing [this previous post](https://rogerkimjazzlover.github.io/django/django-html-features/), I faced a jekyll syntax error. I am currently writing my posts using the [Minimal Mistakes Jekyll Theme](https://github.com/mmistakes/minimal-mistakes); and I faced the _"Liquid Exception: Liquid syntax error: Unknown tag 'some_tag' in post_file_directory"_.

## Reason

In [this previous post](https://rogerkimjazzlover.github.io/django/django-html-features/), I talked about html features provided by django. Like this:

[//]: # {% raw %}
```
{%load static%} #This
{%include "navbar.html"%} #Or this
```

***The problem was that*** the Jekyll Liquid engine mistakenly treated the ```{% django-stuff %}``` as Jekyll tags, even when they were enclosed within the _"```"_ code blocks. Since these tags are specific to django and cannot be understood by the Jekyll engine, it resulted in a build failure.

[//]: # {% endraw %}

## Solution

If you search this issue up in google, or ask Chat-GPT like I did, the solutions would be to add 

[//]: # {% raw %}

_{% raw %}_ and _{% endraw %}_ tags before the code. Like this:

[//]: # {% endraw %}

[//]: # {% raw %}

```
{% raw %}
{% load static %} # Do this
<!DOCTYPE html>
...
    <link rel="stylesheet" href="{% static 'ui/name.css' %} # and something like this
...
{% endraw %}
```

[//]: # {% endraw %}

***However,*** that didn't work for me. Instead, I had to add

[//]: # {% raw %}

```[//]: # {% raw %}``` and ```[//]: # {% endraw %}``` tags instead of the plain 

[//]: # {% endraw %}

[//]: # {% raw %}
- _{% raw %}_ and 
- _{% endraw %}_ tags.

[//]: # {% endraw %}

## Conclusion

The original solution might work just fine for you, but if it doesn't, it's certainly worth to try out my solution.

## Contact Me:

Roger Kim

[Github](https://github.com/RogerKimJazzLover)

e-mail: <minseungkim1017@gmail.com> 
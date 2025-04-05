---
layout: single
title: "Jekyll Liquid Syntax Error"
categories: bugs
tag: [bug-fix]
---

## Introduction

When I was writing [this previous post](https://kmsrogerkim.github.io/django/django-html-features/), I faced a jekyll syntax error. I am currently writing my posts using the [Minimal Mistakes Jekyll Theme](https://github.com/mmistakes/minimal-mistakes); and I faced the _"Liquid Exception: Liquid syntax error: Unknown tag 'some_tag' in post_file_directory"_.

## Reason

In [this previous post](https://kmsrogerkim.github.io/django/django-html-features/), I talked about html features provided by django. Like this:

[//]: # {% raw %}
```
{%load static%} #This
{%include "navbar.html"%} #Or this
```

***The problem was that*** the Jekyll Liquid engine mistakenly treated the ```{% django-stuff %}``` as Jekyll tags, even when they were enclosed within the _"```"_ code blocks. Since these tags are specific to django and cannot be understood by the Jekyll engine, it resulted in a build failure.

[//]: # {% endraw %}

## Solution 1

If you search this issue up in google, or ask Chat-GPT like I did, the solutions would be to add 

&#123;% raw %&#125; and &#123;% endraw %&#125; tags before the code. Like this:

&#123;% raw %&#125;
```
djang-stuff-code
```
&#123;% endraw %&#125;

## Solution 2

***However,*** that didn't work for me. Instead, I had to add

***&#91;//&#93;: # &#123;% raw %&#125;***

and 

***&#91;//&#93;: # &#123;% endraw %&#125;***

tags instead.

## Solution 3

Or, you can just simply use corresponding HTML entities. 
- ```{``` as ```&#123;```, 
- and ```}``` as ```&#125;``` 

&#123;% raw %&#125; = ```&#123;% raw %&#125;```

## Conclusion

The original solution might work just fine for you, but if it doesn't, it's certainly worth to try out my solution.

## Contact Me:

Roger Kim

[Github](https://github.com/kmsrogerkim)


---
layout: single
title: "Github Actions to Automate Image pushing & Django Testing"
categories: devops
tag: [django, docker, aws, devops, ci/cd, github actions] 
---
## Introduction 
In this post, I would like to discuss how I set up a CI/CD pipline for my [toyki](https://toyki-homepage.vercel.app/)project. I automated unit testing for my backend application built with Django, and the process of creating a docker image of it and pushing it to AWS ECR, all using GitHub actions.

## Getting Started
To set up a GitHub Actions workflow, go to the `Actions` tab in your repository and click `New Workflow`. Choose a template, configure the .yml file, and commit it. This automatically creates a `.github/workflows/` directory containing the .yml files, which define your workflows.

Alternatively, you can manually create the `.github/workflows/` directory and add .yml files yourself, and GitHub will recognize and run them.

Here's how the beginning of the .yml files would look like. As you can see below, you can configure when your workflows will run. The .yml below shows that the name of the workflow is `Django CI` and it will run when 

1. a commit is pushed to the `main` or the `development` branch
2. when a pull request is created on them.

```yml
name: Django CI

on:
  push:
    branches: [ "main", "development" ]
  pull_request:
    branches: [ "main", "development" ]
```

## Automate Unit Tests
So first, I created unit tests for my REST API, using pytest. Then I created a .yml file in the `.github/workflows/` directory which looks something like this.

```yml
name: Django CI

on:
  push:
    branches: [ "main", "development" ]
  pull_request:
    branches: [ "main", "development" ]

jobs:
  test:
    runs-on: ubuntu-latest

    services:
      postgres:
        image: postgres:14-alpine
        env:
          POSTGRES_DB: toyki
          POSTGRES_USER: your_usr_name_here 
          POSTGRES_PASSWORD: your_pass_here
        ports:
          - 5432:5432
      memcached:
        image: memcached:1.6.14-alpine
        ports:
          - 11211:11211

    strategy:
      max-parallel: 4
      matrix:
        python-version: ['3.10']

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python ${{ matrix.python-version }}
        uses: actions/setup-python@v3
        with:
          python-version: ${{ matrix.python-version }}

      - name: Install Dependencies
        run: |
          python -m pip install --upgrade pip
          pip install poetry
          poetry install

      - name: Generate Environment Variables File
        run: |
          echo "DJANGO_SECRET_KEY=$DJANGO_SECRET_KEY" >> .env.dev
          echo "API_KEY=$API_KEY" >> .env.dev
        # other sensitive env variables that are stored in Github secrets

        env:
          DJANGO_SECRET_KEY: ${{ secrets.DJANGO_SECRET_KEY }}
          API_KEY: ${{ secrets.API_KEY }}
          # also declare your env variables here
          # so that the python's .load_env() would get them

      - name: Run Tests
        run: |
          poetry run pytest <your directory to the test code file>
        # e.x: tests/test_django.py

        env:
          ENVIRONMENT: 'development'
          ALLOWED_HOST: '*'
          DEBUG: 'True'
          # other env variables that are not sensitive and
          # can directly be stored as text in .yml file
```
## Conclusion

## Contact Me:
Roger Kim

[Github](https://github.com/kmsrogerkim)

e-mail: <minseungkim1017@gmail.com> 


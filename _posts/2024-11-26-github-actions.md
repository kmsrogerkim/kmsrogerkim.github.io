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
        # necessary env variables to set up your postgreSQL db
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
        # other sensitive env variables that are stored in Github secrets

        env:
          DJANGO_SECRET_KEY: ${{ secrets.DJANGO_SECRET_KEY }}
          API_KEY: ${{ secrets.API_KEY }}
          # declare your env variables here
          # so that the system can reach them on the command above with the $ sign

      - name: Run Tests
        run: |
          poetry run pytest <your directory to the test code file>
        # e.x: tests/test_django.py

        env:
          ENVIRONMENT: 'development'
          # other env variables that are not sensitive and
          # can directly be stored as text in .yml file
```

- `services`
  - These services can be used for the steps that follow; in this case unit testing.
- `strategy`
  - `max-parallel`: this configures how many runs can run simultaneously (parallel)
  - `matrix`: sets up some variables that can be used through out the run
- `steps`
  - This sections basically states what the github actions will do. It is very similar to how Dockerfile works if you think about it. You just tell the container to run certain commads. 
  - The only thing that you might not be familiar with would be the `uses` command used along with `actions/checkout$v4` and `actions/setup-python@v3`
- `secrets`
  - The secret env variables can be set in `github.com/your_id/your_repo/settings/secrets/actions`path.
  - And they can be reacehd by doing `${{ secrets.sth }}` as can see from above.
- `uses`
    - This keyword specifies an action to be executed as part of the workflow. Actions, just like the one we are creating right now, are pre-built, reusable units of code that perform specific tasks.
    - `actions/checkout@v4`: an actions maintained by GitHub that checks out the code from the repository to whatever the envrionment the actions will be ran (upload it to VM).
    - `actions/setup-python@v3`: It sets up a Python environment in the runner. It ensures that the specified version of Python is installed and available in the `PATH`, which, if you have ever tried setting up Python on different machines, can sometimes be a huge pain in the ass. 

## Automate Image Pushing to AWS ECR
If you click on the `New Workflow` button in the actions tab, you can see `Deploy to Amazon ECS`. This action already includes image creation and pushing to ECR. So I just used that. Here's how it looks like.

```yml
name: Push Image to ECR

on:
  push:
    branches: [ "main" ]

env:
  AWS_REGION: your_region_here
  ECR_REPOSITORY: your_ecr_name_here
  # e.x: toyki

permissions:
  contents: read

jobs:
  push_image:
    name: push-image
    runs-on: ubuntu-latest
    environment: production
    # set the env variable of `envronment` to production
    # since some of my codes runs differently depending on this
    # env variable

    steps:
    - name: Checkout
      uses: actions/checkout@v4

    - name: Configure AWS credentials
      uses: aws-actions/configure-aws-credentials@v1
      with:
        aws-access-key-id: ${{ secrets.AWS_ACCESS_KEY_ID }}
        aws-secret-access-key: ${{ secrets.AWS_SECRET_ACCESS_KEY }}
        aws-region: ${{ env.AWS_REGION }}

    - name: Login to Amazon ECR
      id: login-ecr
      uses: aws-actions/amazon-ecr-login@v1

    - name: Build, tag, and push image to Amazon ECR
      id: build-image
      env:
        ECR_REGISTRY: ${{ steps.login-ecr.outputs.registry }}
      run: |
        DJANGO_IMAGE_TAG=$(cat django_image_tag.txt)
      # I specify the image tag for my production images in a text file
      # in the repository. It is updated everytime a PR is merged to main

        docker build -t $ECR_REGISTRY/$ECR_REPOSITORY:$DJANGO_IMAGE_TAG .
        docker push $ECR_REGISTRY/$ECR_REPOSITORY:$DJANGO_IMAGE_TAG
        echo "image=$ECR_REGISTRY/$ECR_REPOSITORY:$DJANGO_IMAGE_TAG" >> $GITHUB_OUTPUT
```
There is nothing special here. There are a lot of pre-built actions from aws themselves that you can use in your GitHub actions. For example, the `aws-actions/configure-aws-credentials` and `aws-actions/amazon-ecr-login@v1` actions are used in this action.

## Conclusion
While doing this, I felt like everything is just a bash script at its core. GitHub sets up an isolated environment for you either using VM (default) or containers. Then you tell the machine to run some commands. Just like Dockerfile, and just like a bash script. 

In fact, I am currently doing another project with the HYU's Vibro Acoustics lab, where I have to manually set up Docker and everything in an EC2 instance. In the process, I made up a bash scrip of my own that automates a lot of the set up process. I also created a bash script that pulls image from ECR and set up some variables and run the image as container. While I was doing that, I thought to myself that maybe this is just what is happening behind the scene for AWS's ECS service at its core.

Anyways, I hope my post helped make your developing life better.

## Written by
Roger Kim [[GitHub](https://github.com/kmsrogerkim)] [[LinkedIn](https://www.linkedin.com/in/kmsrogerkim/)] 


# Annotations
The one-line GitHub Action to remotely trigger a job on Jenkins. You just need to pass 3 parameters to get it working:

| Parametr  | Description |
| ------------- | ------------- |
| JENKINS_URL  | URL of a Jenkins instance with specified job's path |
| JENKINS_USER  | User from whose identity an API will be called |
| JENKINS_API_KEY  | User's valid API key |


## How to use
Here is a example of how to trigger Jenkins job on every push to the staging or dev branch:
```yaml
name: Trigger Job on Jenkins
on:
  push:
    branches:
       - staging
       - dev

jobs:
  trigger:
    name: Trigger
    runs-on: ubuntu-latest

    steps:
    - uses: devkyt/jenkins-trigger@main
      with: 
        JENKINS_URL: https://my.jenkins.com/job/Pipelines/job/Frontend/buildWithParameters?BRANCH=dev&ENVIRONMENT=dev
        JENKINS_USER: jenkins
        JENKINS_API_KEY: set324sfvokom87ldfs
```

#### About URLs
The default job's URL looks like this: ```https://my.jenkins.com/job/Backend/build```.<br>

But if your job supports input parameters  then you should use ```buildWithParameters``` instead of the ```build``` at the end of the path. Even if you don't want to run the job with some actual params. Otherwise, you can provide them as a query ```https://my.jenkins.com/job/Backend/buildWithParameters?BRANCH=dev&ENVIRONMENT=dev```. 

Below you will find a few examples of Jenkins job URLs.

| Type  | Example |
| ------------- | ------------- |
| Common  | https://my.jenkins.com/job/Backend/build |
| Multibranch  | https://my.jenkins.com/job/Pipelines/job/Frontend/buildWithParameters |
| Common with params  | https://my.jenkins.com/job/Backend/buildWithParameters?BRANCH=dev&ENVIRONMENT=dev |
| Multibranch with params  | https://my.jenkins.com/job/Pipelines/job/Frontend/buildWithParameters?BRANCH=dev&ENVIRONMENT=dev|

# Delio DevOps Senior Engineer Test

Delio Engineering have made the decision to start selling "Delio" branded hoodies and coasters. We have developed an API back-end written in Node JS and a simple HTML front-end frontend. 

## The task

It's your job to create the infrastructure for this new site. To complete this task, you'll need to:

* Use "infrastructure as code" to create the infrastrucure in either AWS or Azure. 
* Deploy the API within a Kubernetes cluster.
* Deploy the frontend to static hosting.
* Show a clear commit history and an understand of Git.
* Document any decisions you've made and why.

Optional extras:

* Add unit tests to your code.
* Create a deployment pipeline.

## The rest

Please do not hesitate to get in touch with any questions you have during the process.

## README Begins Here 

### 1. Create branches using a git flow branching strategy, master -> dev -> feature -> dev -> master 

### 2. Create infrastructure on AWS with infastructure orchestration tool terraform

Requirements / Tools Used:

* awscli
* aws credentials saved in ~/.aws/credentials | configured
* docker
* terraform
* kubectl 

### 3. Package app into docker

### 4. Deploy app on EKS 

### 5. Setup jenkins pipeline for deploying docker app onto eks

### 6. Have fun ;)

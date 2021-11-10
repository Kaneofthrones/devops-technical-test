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

For additional info see [wiki page](https://github.com/Kaneofthrones/devops-technical-test/wiki)

Requirements / Tools Used:

* awscli
* aws credentials saved in ~/.aws/credentials | configured
* docker
* terraform
* kubectl
* nodejs
* npm

keep in mind certain files have been excluded as standard code practise these are:

     node_modules/*
     terraform/.terraform/*
     terraform/kubeconfig*

### 1. Create branches using a git flow branching strategy, master -> dev -> feature -> dev -> master 

### 2. Create infrastructure on AWS with infastructure orchestration tool terraform

eks-cluster.tf will clone another git repo that has the source code for eks

### 3. Package app into docker

make dockerfile for app.js

run app to check docker image works

    docker run -p 49160:3000 -d km-node-app

Curl to verify app is behaving, you should see "hello world"

    curl -i localhost:49160 

### 4. Deploy app on EKS & static host the html file

To deploy on EKS:

    kubectl apply -f kubed-app

the container is on my dockerhub account (kaneofthrones) if it cant be found locally

Then to check the app is running:

    kubectl get pods --watch

Once its running run the following to get the loadbalancer address

    kubectl get svc

copy the external ip of the load balancer into your web browser to be greated with "hello world"



Static host html file:

 static hosting on eks

![delio_1](https://user-images.githubusercontent.com/30622959/140850493-c70b6428-ef48-40d8-b6f6-353e12becb02.png)


### 5. Setup jenkins pipeline for deploying docker app onto eks

Run the following to install an efs file system

    aws efs create-file-system \
    --creation-token creation-token \
    --performance-mode generalPurpose \
    --throughput-mode bursting \
    --region eu-west-2 \
    --tags Key=Name,Value=KMEFSFileSystem \
    --encrypted

run following to create mount targets in the AZ's:

    aws efs create-mount-target \
    --file-system-id <id> \
    --subnet-id <id> \
    --security-group <id> \
    --region eu-west-2

create access point:

    aws efs create-access-point --file-system-id <id> \
    --posix-user Uid=1000,Gid=1000 \
    --root-directory "Path=/jenkins,CreationInfo={OwnerUid=1000,OwnerGid=1000,Permissions=777}"

Deploy CSI driver for eks cluster 

    kubectl apply -k "github.com/kubernetes-sigs/aws-efs-csi-driver/deploy/kubernetes/overlays/stable/?ref=master"

### 6. Have fun ;)

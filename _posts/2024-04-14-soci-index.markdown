---
title: "How SOCI Index Reduced my Image Load Times by 70%"
date:   2024-04-14 00:00:00 +1000
tags: 
  - AWS
  - Docker
  - ECS
comments: true
classes: wide
#header: 
#  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/AWS-Certified-Solutions-Architect-Associate_badge.3419559c682629072f1eb968d59dea0741772c0f.png
---
# Introduction
Hello my fellow Docker-AWS-developing folks! I got some good stuff to share with you today. 

Do you have large (1GB+) images that takes _ages_ to pull?

Does this image take longer to **setup** than to run the main process?

Large images are a big problem when you want tasks to be done in a set amount of time. This is especially the case when you use [AWS Fargate](https://aws.amazon.com/fargate/), where tasks are spun up and shut down each time. You don't want your tasks to be sitting around waiting for the image to download!

We're here to save **time and money**!!!!! And that is exactly what we're doing today.

I have found a great tool to save **up to 70%** of time when pulling my Docker images.

Without further ado, let me introduce to you: SOCI Index on AWS!

# Background Info
But before I delve into the intricacies of SOCI indices, let me lay out some background information.

## Docker
Docker is a PaaS product that allows developers to package applications in a portable way. Applications in Docker are run inside containers, which can be thought of as lightweight virtual machines. It holds everything that the app needs to run - code, libraries, dependencies and even the OS! This container can be moved and run on any machine that has Docker installed. 

Docker images are templates for creating the containers. It has all the instructions required to create the container. Docker images are typically built from a base image and have extra instructions to suit the use case. 

## ECR
Amazon ECR (Elastic Container Registry) is a fully-managed AWS service that allows users to store Docker images in AWS. You get all the fully-managed AWS benefits: highly available, durable and minimal operational overhead. 

Since it is offered in AWS, it integrates with other AWS services very well. For example, you can apply permissions to your IAM users to set access controls to your docker images. You can also deploy your images in ECR to container orchestration services like ECS and EKS very easily. You can even deploy your docker images to Lambda as well. 

## ECS
Amazon ECS (Elastic Container Service) is a fully-managed AWS service that allows users to run their docker containers. With ECS, its really easy to deploy, manage and scale docker containers on AWS!

You can specify the CPU, memory and networking configurations for your applications, and schedule your containers with ease as well. You can even set it to autoscale based on your performance metrics too!

Integrate this with ECR to easily access your docker images and run them seamlessly.

## Fargate
Amazon Fargate is a compute offering from AWS, available in ECS. It's a serverless offering, meaning you can run your containers without having to manage EC2 instances. Just specify the CPU and memory and off you go! Don't worry about setting up servers.

# The Problem
Now that the background information is out of the way, let me discuss my use case.

I have a Data Science team who wants to run some simulations on AWS. They have kindly created a **Docker Image** to package their application code. I have stored the image to **ECR** - Its pushed and ready to go. 

Our data scientists wants to run their simulation once every 5 minutes. That's perfect, because we can use **ECS** with **Fargate** to spin up the docker container, run the simulation and shut down after its finished. We are only paying for when the simulation is running. 

The team also needs to run their simulation within **two minutes**. That is fine, because when we tested it locally the simulations only took **a minute!**

...hang on a minute. When I run it on AWS, its taking **two and a half minutes!** What's going on?

## Diagnosing the problem
The `aws cli` can give us a hint on what is going on. 

`aws ecs describe-tasks --tasks <TASK_ID>`

The output might look something like this:
```
{
    "version": "0",
    "detail-type": "ECS Task State Change",
    "source": "aws.ecs",
    "region": "ap-southeast-2",
    "resources": [
        "arn"
    ],
    "detail": {
        "attachments": [
            {
                "type": "eni",
                "status": "DELETED",
                "details": [
                    {
                        "name": "subnetId",
                        "value": "subnet"
                    },
                    {
                        "name": "networkInterfaceId",
                        "value": "eni"
                    },
                    {
                        "name": "macAddress",
                        "value": "mac"
                    },
                    {
                        "name": "privateDnsName",
                        "value": "ip"
                    },
                    {
                        "name": "privateIPv4Address",
                        "value": "ip"
                    }
                ]
            }
        ],
        "attributes": [
            {
                "name": "ecs.cpu-architecture",
                "value": "x86_64"
            }
        ],
        "availabilityZone": "ap-southeast-2b",
        "clusterArn": "arn",
        "connectivity": "CONNECTED",
        "connectivityAt": "date",
        "containers": [
            {
                "containerArn": "arn",
                "exitCode": 0,
                "lastStatus": "STOPPED",
                "name": "name",
                "image": "image",
                "imageDigest": "sha256:",
                "runtimeId": "id",
                "taskArn": "arn",
                "networkInterfaces": [
                    {
                        "attachmentId": "",
                        "privateIpv4Address": ""
                    }
                ],
                "cpu": ""
            }
        ],
        "cpu": "16384",
        "createdAt": "",
        "desiredStatus": "STOPPED",
        "enableExecuteCommand": false,
        "ephemeralStorage": {
            "sizeInGiB": 20
        },
        "executionStoppedAt": "",
        "group": "",
        "launchType": "FARGATE",
        "lastStatus": "STOPPED",
        "memory": "32768",
        "overrides": {
            "containerOverrides": [
                {
                    "name": ""
                }
            ]
        },
        "platformVersion": "1.4.0",
        "pullStartedAt": "2024-04-12T05:56:00.171Z",
        "pullStoppedAt": "2024-04-12T05:57:30.739Z",
        "startedAt": "2024-04-12T05:57:32.323Z",
        "startedBy": "",
        "stoppingAt": "2024-04-12T05:58:35.034Z",
        "stoppedAt": "2024-04-12T05:58:49.111Z",
        "stoppedReason": "Essential container in task exited",
        "stopCode": "EssentialContainerExited",
        "taskArn": "",
        "taskDefinitionArn": "",
        "updatedAt": "2024-04-12T05:58:49.111Z",
        "version": 5
    }
}
```

We are interested in the time - especially `pullStartedAt` and `pullStoppedAt`. If you take a look, it shows that the image took **a minute and a half** to pull! 

That's not good! We want our simulations to finish in 2 minutes, but its taking 1.5 minutes just to get ready!
We need a way to speed up the startup process. This is where SOCI index comes in.

## SOCI Index
*Seekable Open Container Initiative* (SOCI) is an add-on technology within the docker ecosystem. It allows **lazy loading** of container images, meaning images can be pulled and loaded faster than conventional methods.

When you use SOCI, you first create a **SOCI index** for your image. The index puts a priority on the files and layers inside your image. This allows only the necessary portions of the image to be downloaded on-demand when setting up the image, rather than downloading the whole thing before starting up. 

SOCI can also track the location of files within the compressed image layers. When a file is accessed, only the relevant compressed chunks containing the file are downloaded and decompressed, so that the download and decompression operations are kept at a minimum. 

Overall, its a very innovative technology that enable on-demand loading of your images. This improves the startup performance and efficiency for Docker containers.

If you want to read more about SOCI indexes, check out this AWS Blog Post here: https://aws.amazon.com/blogs/containers/under-the-hood-lazy-loading-container-images-with-seekable-oci-and-aws-fargate/

## Using it on AWS
In order to utilise the SOCI technology, we first have to create the SOCI indexes from our Docker images. 

To do this, we have to install and use some SOCI software to generate the indexes and push it to our image repositories. 

Thankfully, AWS has created a Github Repo with Cloudformation stacks that will deploy a SOCI Index Builder on your account. 

This stack will deploy Lambda functions and EventBridge rules in your AWS account. These resources will automatically detect new images being pushed into your ECR repositories, create SOCI indexes for them and push the index into the same ECR repository. 
When using a SOCI indexed image, there is nothing special that you have to do. You can pull images from ECR just like you would normally do and you can see a boost in performance straight away. ECR will automatically use the SOCI index that is tied to your image to improve its performance.

For more information about AWS's SOCI Index Builder, refer to https://aws-ia.github.io/cfn-ecr-aws-soci-index-builder/

## My Use Case
As an example, when I first tried out SOCI indexes, I had a Docker image that was around 1GB in size.
When I pull the image normally, my Fargate tasks take about **60 seconds** to start up.

When I used SOCI indexes, the time was cut down to **15 seconds**!! That is a 75% improvement.

Note that your experience with SOCI Index may vary based on the size of your Docker images. Official documentation recommend using SOCI index for any image larger than 250MB. Anything less and you are not likely to see a time reduction.

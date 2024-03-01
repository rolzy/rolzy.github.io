---
title:  "Studying for the AWS Solution Architect Associate Exam"
date:   2024-03-01 00:00:00 +1000
tags: 
  - AWS
  - Certifications
comments: true
classes: wide
header: 
  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/splash-images/linux_alias-1280.png
---
# Courses
I took the [A Cloud Guru Solution Architect Associate](https://learn.acloud.guru/course/certified-solutions-architect-associate/dashboard) course for the bulk of my study. It was an exceptional curriculum that had just the right amount of theory and hands-on labs. The theory was taught in short videos which made the experience very engaging. The lectures also made the content engaging thanks to their casual tone. Any complex terminologies were explained in easy words so the material was easy to follow. 

The hands-on labs in the courses were done in a small AWS environment where you can actually play around with the AWS console and services. I had no technical issues when running the labs. The instructions for the labs were clear, but not too clear as to give away the answers. It was kept at a good difficulty. Also, their labs were designed based on real-life scenarios which made it further engaging for me.

# Study topics
I like how ACG divided the materials up into service categories. I would recommend doing this, it helps to learn ALL the AWS services and get your head around why each service exist. 
I used the following categories for my notes:
- Automation
    - Anything that automates your workflows on the Cloud. EventBridge, Cloudformation
- Big Data
    - Data analytics and machine learning. Sagemaker, Lakeformation, Redshift, EMR, etc
- Compute
    - EC2, Lambda
- Containers
    - ECS, ECR, Kubernetes
- Cost Management
    - Billing, Cost explorer
- Databases
    - RDS, Aurora
- Decoupling
    - SQS, SNS
- Management & Governance
    - IAM, Organizations 
- Migration
    - Migrating from on-prem to cloud
- Monitoring
    - CloudWatch, CloudTrail
- Networking
    - VPC
- Security
    - Security Groups, firewalls, Shield, Inspector, GuardDuty
- Storage
    - S3, EFS, EBS

# Practice Exams
Don't be afraid of looking at the answers! When studying, make an educated guess, compare to the answer, and make sure to understand why you're wrong if you are wrong. Going through a whole practice exam without knowing if you're correct or not is a waste of time. Its hard to go over each question one by one. Its better to get a feedback loop going at smaller intervals. 

There are quite a few trick questions in the exam. Make sure to extract key words when answering a question. Words like Serverelss, scale out, securely are keywords to look out for. Big hints are at the end of the question. Look out for phrases like Cost Effectively, Operational overhead, code changes etc. 

Take your time to read the question - there is plenty of time in the exam. 

During practice, when you get a question wrong, don't beat yourself too much. Even if you got tricked, as long as you had a reason for your answer, thats still important. 

# Front-end, Back-end and everything in between
A lot of emphasis on making software modular. How can the software be broken down? Think about front-end and back-end. Which services fit into front-end? Which services are for back-end? Which services sit in between and allow the two to communicate to each other? Which services support the project as a whole?

Understanding the purpose that each service serves will also help you in understanding all the services. 

# My pick of services to look out for
Here are 5 services that AWS loves and tend to be an answer in the exam:
- SQS omg if SQS is one of the choices, its probably the answer
- CloudFront: It can do anything - deliver content worldwide, failover, cook your dinner, fix your broken marriage...
- Lambda: Duh
- VPC: Its what makes everything work together
- DynamoDB: RDS is a bigger service, but the serverless DynamoDB is AWS's favourite database offering IMO


<!-- 
- Introduction
    - I recently took the Associate Solution Architect exam
    - Share my tips and tricks from my study
- Study courses
    - The A Cloud Guru course
    - Good course! Up to date
    - Video for each service (popular services have their own segment)
        - Easy to segregate study 
    - Each instructor have their own style, makes it more interesting
- Study topics
    - Divide to service categories
    - Automation, Big Data, Compute, Cost Management, Databases, Decoupling, Management & Governance, Migration, Monitoring, Networking, Security, Storage 
    - Divide and conqurer
- Practice exams
    - Looking at each question, make an educated guess, check against answer
        - If you're wrong, study and understand why you're wrong
    - Some questions are gotchas
        - Extract key words
            - Serverless, scale out seamlessly, securely...
            - Especially the last few words
            - Cost effectively, operational overhead, code changes, 
        - Take your time to read the question. Plenty of time in exam
        - Don't beat yourself too much
- The frontend-backend construct
    - A lot of emphasis on frontend, backend and segmentation
    - Microservices and using queues
    - The networking to put it all together
- Services to look out for
    - SQS
    - CloudFront
    - Lambda
    - VPC
    - DynamoDB
-->

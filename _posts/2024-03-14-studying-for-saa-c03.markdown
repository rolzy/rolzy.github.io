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
# Introduction
I recently passed the [AWS Solution Architect - Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/) exam! In this article, I will share you my two cents on the exam, as well as any tips that I think you should consider when studying for this exam. 

# How I Studied for the Exam
I took two steps to study for the exam. 

Firstly, I took a course offered by A Cloud Guru to learn about each and every AWS service covered by the course. I watched every lecture, did every lab and took notes from the classes. 

Secondly, I did *a ton* of practice exams. I did the ones offered by A Cloud Guru, and any other free ones that I could find. I checked my answers against other users, and researched on the ones that I got wrong. 

# Course
I'll first go over my first step of my Solution Architect journey.

For study materials, I took the [A Cloud Guru (ACG) AWS Certified Solution Architect Associate](https://learn.acloud.guru/course/certified-solutions-architect-associate/dashboard) course. This was the bulk of my study. I think it was an excellent course, it had just the right amount of theory and hands-on labs. The theory was taught in short videos which made the experience very engaging. The lectures also talk in this friendly and casual tone, which makes the classes fun as well. Any complex terminologies were explained in simple terminology. Overall, the course was very easy to follow.

In the past, I've tried courses where the theory was taught purely in text, and it was so boring that I couldn't finish the course. ACG's course is the opposite. Its fun and engaging, which is exactly what you need when studying the vast world of AWS.

The hands-on labs in the courses were done in a small AWS environment where you can actually play around with the AWS console and services. The console was identical to the one you see in AWS. I had no technical issues when running the labs. 

The labs are based on real-life scenarios, like "hosting a static website on a S3 bucket" or "setting up a VPC with an internet gateway". This gave me an idea as to how AWS services could and should be used. The instructions for the labs were clear, but not too clear as to give away the answers. They also had a "challenge mode" available for those who wanted to do the labs without instructions. 

### Study Topics
If I were to take one thing from the ACG course, its how they divided the study materials up into service categories. I would recommend doing this even if you are not taking the ACG course. It helps when you are trying to get your head around the plethora of AWS services that is available today.

Here is how I would divide up the exam study:
- **Automation**: Anything that automates your workflows on the Cloud. Things like EventBridge and Cloudformation
- **Big Data**: Data analytics and machine learning. Sagemaker, Lakeformation, Redshift, EMR, etc
- **Compute**: Things that run code. EC2 and Lambda
- **Containers**: All things docker. ECS, ECR, Kubernetes
- **Cost Management**: Services to help you manage AWS costs. Billing, Cost explorer are the main ones
- **Databases**: There are many database services in AWS. The main ones are RDS, Aurora, DynamoDB
- **Decoupling**: Services you use between a server and another server. Think SQS and SNS
- **Management & Governance**: Where you do admin stuff. IAM, Organizations, Control Tower
- **Migration**: Services you use when migrating from on-prem to cloud. XXX Migration Service, Datasync, the Snow series, etc
- **Monitoring**: Where logs and metrics are stored. Things like CloudWatch, CloudTrail
- **Networking**: VPC and everything beneath it
- **Security**: There are many services here. Security Groups, firewalls, Shield, Inspector, GuardDuty
- **Storage**: Where you store data. S3, EFS, EBS


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
- Make sure to study each course, even if you think you know it. The course is taught with the exam in mind so that perspective will shine a new light to the AWS service that you think you know.
-->

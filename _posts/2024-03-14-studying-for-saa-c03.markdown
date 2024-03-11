---
title:  "Studying for the AWS Solution Architect Associate Exam"
date:   2024-03-01 00:00:00 +1000
tags: 
  - AWS
  - Certifications
comments: true
classes: wide
header: 
  teaser: https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/teaser-images/AWS-Certified-Solutions-Architect-Associate_badge.3419559c682629072f1eb968d59dea0741772c0f.png
---

![Study](https://rolzy-blog-assets.s3.ap-southeast-2.amazonaws.com/splash-images/pexels-lumn-167682.jpg)

# Introduction
I recently passed the [AWS Solution Architect - Associate](https://aws.amazon.com/certification/certified-solutions-architect-associate/) exam! In this article, I will share my two cents on the exam and any tips that I think you should consider when studying for this exam. 

# How I Studied for the Exam
I took two steps to study for the exam. 

Firstly, I took a course offered by A Cloud Guru to learn about each and every AWS service covered by the exam. I watched every lecture, did every lab and took notes from the classes. 

Secondly, I did *a ton* of practice exams. I did the ones offered by A Cloud Guru, and any other free ones that I could find. I frequently checked my answers and researched on the ones that I got wrong.

# First step - Taking an online course
First off, I took the [A Cloud Guru (ACG) AWS Certified Solution Architect Associate](https://learn.acloud.guru/course/certified-solutions-architect-associate/dashboard) course. This was the bulk of my study. I think it was an excellent course, it had just the right amount of theory and hands-on labs. The theory was taught in short videos which made the experience very engaging. The lectures also talk in this friendly and casual tone, which makes the classes fun as well. Any complex terminologies were explained in simple words. Overall, the course was very easy to follow.

In the past, I've tried courses where the theory was taught purely in text - it was so boring that I couldn't finish the course. ACG's course is the opposite. Its fun and engaging, which is exactly what you need when studying for a big exam like this one.

The hands-on labs in the courses were done in a small AWS environment where you can actually play around with the AWS console and services. The console was identical to the one you see in AWS. I had no technical issues when running the labs. 

The labs are based on real-life scenarios, like "hosting a static website on a S3 bucket" or "setting up a VPC with an internet gateway". This gave me an idea as to how AWS services could and should be used. The instructions for the labs were clear, but not too clear as to give away the answers. They also had a "challenge mode" available for those who wanted to do the labs without instructions. 

### Study Topics
The best thing about ACG's course is how the study material is divided into service categories. I would recommend doing this even if you are not taking the ACG course. It helps when you are trying to get your head around the plethora of AWS services that is available today.

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

# Second step - Practice exams
Once I finished the A Cloud Guru course, I moved on to practice exams. I did a ton of these.

The first point I'd like to make is this: don't be afraid of looking at the answers! When studying for an exam, a lot of people try and avoid looking at the answers until they finish the whole exam. Some online practice exams are formatted like this as well. 

When I study, I prefer to look at each question, make an educated guess and compare the answers before I move on to the next question. If I get a question wrong, I make sure to go over the materials and understand why I went wrong. This way, the thought process for the question is still fresh in my mind. If I'm reviewing answers at the very end of a 65-question exam, not only am I mentally exhausted, but I won't remember why I chose the wrong answers. I like to have small and frequent feedback loops for my studies. 

Also, there are quite a few trick questions in the exam. To avoid getting tricked, make sure to extract key words when answering a question. In particular, big hints are at the end of the question, where it describes how they want to perform a job. For example, if the question ends with "most cost effectively", you will prioritize choices that are cheap, such as EC2 spot instances and serverless options. If the question is about migrating an on-prem monolithic application and it asks for the "least amount of code changes", you wouldn't try and redesign the whole application, but rather look at running the same code on an EC2 instance.

### My pick of services to look out for
Here are 5 services that AWS loves and tends to be an answer in the exam:

5. DynamoDB - Its got all the buzzwords in it. NoSQL, infinitely scalable, it even has a serverless offering now too!
4. VPC - This service is way too big. You need to learn some networking if you want to pass this exam.
3. Lambda - Does this need an introduction? If you want to run code easily, use Lambda
2. CloudFront - It's so much more than a content delivery service. It can do failover, serving content, edge computing, cook your dinner, fix your car.
1. SQS - For some reason AWS loves this thing. If SQS is one of the choices, I can guarantee SQS is the answer for your question. At least in 2024.
{: reversed="reversed"}

### Conclusion
That's a wrap! Study hard, prep hard and good luck with your AWS certification journey :)

---
title: DevOps
media_order: cc.png
taxonomy:
    category:
        - DevOps
        - Personal
---

[TOC]

## Preface

DevOps can usually unleash its full potential in combination with [Cloud Computing](#cloud-computing) and [Infrastructure as Coe](#infrastructure-as-code), which are described in the following article as well.

## Terms and definitions
! Disclaimer
This page describes certain aspects in the area of DevOps. If not marked these statements are my own wording based upon my own thinking and experience without any engagement with respect to correctness and other opinions.

## DevOps

!!! An enterprise **culture** aiming to deliver high quality software within a short lead time and high efficiency taking all the stakeholders into account.

### Dev vs Ops

| What Devs want | What Ops want |
|  :-----          |  :-----          |
| Deliver fast | Ensure availability |
| Deliver frequently | Caution |
| Deliver new features | Stability and Security |

### Principles

**CAMS**<small> by Damon Edwards and John Willis</small>

- **C**ulture
- **A**utomation
- **M**easurement
- **S**haring

### Continuous Everything

**tbd**

## Cloud Computing

!!! Utilization of **dynamic** IT ressources offered by a cloud service platform through a network.

### Types of Cloud Computing Services
Cloud Computing can be distinguished in *infrastructure as a Service*, *Platform as a Service*, *Software as a Service* and *Function as a Service*. The following picture illustrated the main differences ot those types and compares them to classical on premise datacenters.

![Image link](cc.png?link&cropResize=300,400)

Examples in the Amazon ecosystem:

|  Service |  Amazon Product |
|  :-----          |  :-----          |
|  IaaS |  [Amazon Web Services Elastic Compute Cloud (AWS EC2)](https://aws.amazon.com/de/ec2/?nc2=h_m1) |
|  PaaS |  [Amazon Web Services Elastic Compute Cloud Container Service (AWS ECS)](https://aws.amazon.com/de/ecs/?nc2=h_m1) |
|  FaaS | [Amazon Web Services Lambda (AWS Lambda)](https://aws.amazon.com/lambda/)|
|  SaaS[^1] |  [Amazon Web Services SaaS](https://aws.amazon.com/de/partners/saas-on-aws/) |

### Types of Cloud Computing Delievery

| Cloud | Characteristic |
|  :-----          |  :-----          |
| Public Cloud | Reachable from the public internet |
| Private Cloud | Dedicated cloud for a single organization manged internally or externally |
| Hybrid Cloud | Mix of public and private cloud |

### Advantages of Cloud Computing

- No need to invest in data centers
- Pay as much as you consume
- Benefit from reduced costs of scaling effects
- Reduce complexity of capacity planing
- Increase speed and agility
- More focus on business instead of infrastructure

## Infrastructure as Code

!!! Automated management of the life cycle of all infrastructure components in their entirety by utilization of methods and best practices from the area of software engineering.

[^1]: Better known examples for SaaS solutions are Gmail or Office365
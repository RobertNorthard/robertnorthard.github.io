---
title: "Why use Terraform"
layout: post
date: 2019-09-15 12:00
headerImage: false
tag:
- Infrastructure as code
- Terraform 
star: false
category: blog
author: robertnorthard
description: Why use Terraform
---

I am often asked should we use Terraform or the cloud providers native (e.g. AWS CloudFormation, Azure ARM templates).Terraform is great like a software design pattern it provides a common language for orchestrating your infrastructure provisioning. I am fan of the "monorepo" when developing Terraform code for the purpose of  dependency management, versioning all infrastructure code as one version and therefore faster development. It makes sense to decouple modules from the monorepo if they are to be consumed by other parties and are building a centralised asset catalogue.

How does this work? Well the monorepo would consist of a number of number of modules and a single Terraform main.tf file to call these modules. You might also have InSpec tests and a Makefile to orchestrate Terraform commands in a CI / CD pipeline.

But why would you use Terraform over other other infrastructure as code:

### Support for cross cloud and other services

Terraform range of providers let you configure cloud resources from another clouds and further for example Kubernetes clusters enabling you to create that one-click infrastructure and minimise post-provisioning scripts.

### Simple Common Language

Terraform code is simple, the syntax is easy to learn and is easy to make modular code.

### Templateing

The ability to override default values and template files makes it a good candidate for creating multiple-environments from the same code base without changing the code.

Why would you not use Terraform:

### API support

Terraform naturally lags behind he cloud providers API and therefore latest and greatest features and often not available for new services.

### Statefile

You have to manage a statefile. So you have a 'chicken and egg' problem. To use Terraform you need a storage location and to provision this you would need to use the cloud providers native tool of choice. Hashicorp have recently announced Terraform cloud Remote State Management which should resolve this if you are comfortable with them storing the sate file.

### Secretes

The statefile can contain secrets if you are passing them into services. 

### You have a large existing state managed by cloud providers native

Terraform import command will have to be used and is very time consuming.

Do you use Terraform?

~Robert
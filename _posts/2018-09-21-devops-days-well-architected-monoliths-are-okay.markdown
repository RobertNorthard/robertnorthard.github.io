---
title: "Well Architected Monoliths are Okay"
layout: post
date: 2018-09-21 18:00
headerImage: false
tag:
- DevOpsDaysLdn
- DevOpsDays
- Monoliths
- Microservices
star: false
category: blog
author: robertnorthard
description: Lessons learn't on why well architected monoliths are okay at a DevOps Days London Open Space 
---

DevOps Days London was great this year! The talks were interesting and the culture was inclusive and friendly.

I've always thought that we should build the 'correct size service' rather than 'microservices' just for the sake of having them. It is equivalent to using Kubernetes with one docker container - you would have more etcd nodes...

In this blog post I would like to share one of the outcomes of a DevOps days open space discussion on what is / why good monoliths are okay to start with.

So why are well architected and developed monoliths okay:
* Fail fast - they let development teams focus on delivering features (to prove or disprove a hypothesis) rather than a complicated microservice architecture 
* It helps you to understand your requirements (UML diagrams and domain models are not perfect first time they need to evolve) 
* Microservices are complicated to develop (e.g. graceful degradation, health checks, retries) and monitor
* Microservices dependencies are difficult to track

So what does a good monolith look like:
* The code base is modularised by component (e.g. invoices, projects)
* Asynchronous communication between components should use a queue (e.g. RabbitMQ). A single code base is publishing and consuming messages
* If using queues run them in a separate process (e.g. RabbitMQ docker container)

[![Revised Architecture](https://robertnorthard.com/assets/images/21-09-18-monolith.png "Monolith Architecture")](https://robertnorthard.com/assets/images/21-09-18-monolith.png "Monolith Architecture")

Once the application is proven, then it would be a good opportunity to start decomposing if required:
* to support horizontal scaling
* to reduce the risk of deployments
* to distribute development of components of the application to other squads
* simplifies debugging and maintenance
 

What are well architected monoliths?

Participant in the discussion concluded they are a good step for bad monoliths to evolve to before splitting to microservices. This is because the monolith has been battle tested.

~ Robert

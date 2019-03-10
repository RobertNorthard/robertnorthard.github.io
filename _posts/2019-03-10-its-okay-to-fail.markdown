---
title: It's okay to fail
layout: post
date: 2019-03-10 15:00
headerImage: false
tag:
- opinion
 - it's okay to fail
star: false
category: blog
author: robertnorthard
description: it's okay to fail
---

It's okay to fail! If you're not failing you may not be learning effectively. Maybe failing is how you learn best, but perseverance is key. Failing fast is a key principle of DevOps to reduce the impact and risk of failing (e.g. this could be financial by identifying defects earlier).

[![Cost of change](https://robertnorthard.com/assets/images/cost-of-change.jpg "Cost of Change")](https://robertnorthard.com/assets/images/cost-of-change.jpg "Cost of Change")

As a DevOps enthusiast I'm always looking for ways to fail faster. A recent example - I like readable code (we all do) by being well formed and formatted (e.g. using the terraform format command). I  often ignore formatting warnings in my editor and forget to execute unit tests, but it would fail CI. This is waste, we could have failed faster. We should shift further left out of the pipeline and into the IDE so I forced myself to fix errors prior to committing by installing a pre-commit web hook - this can also be shared with the team. Every-time the pipeline breaks, assuming we are following a Trunk-based development approach, the team may stop to fix it, slowing down development.

So what can you do to fail faster and reduce risk:
* Work to a minimum viable product (MVP) 
* Use metrics and data / feedback to guide solutions
* Execute experiments - Hypothesis Driven Development
* Don't over-optimise, not everything needs to be a "golden" solution - as in my previous blog [post](https://robertnorthard.com/devops-days-well-architected-monoliths-are-okay/) building a "well architected monolith" is better than building a custom micro -services that takes 3 months to fail or deliver value

So when you are working on your next project, going out for dinner without a reservation or taking a car for a MOT ask yourself how can you fail faster!

~ Robert

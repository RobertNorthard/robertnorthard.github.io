---
title: Fail faster, it's okay to fail
layout: post
date: 2019-03-10 15:00
headerImage: false
tag:
- opinion
 - it's okay to fail
star: false
category: blog
author: robertnorthard
description: Fail faster! It's okay to fail
---

It's okay to fail! If you're not failing you may not be learning effectively. Maybe failing / making mistakes through trial and error is how you learn best, but perseverance is key. Failing fast is a key principle of DevOps to reduce the impact of failing (e.g. this could be financial by identifying defects earlier - see image below from AgileModeling).

[![Cost of change](https://robertnorthard.com/assets/images/cost-of-change.jpg "Cost of Change")](http://www.agilemodeling.com/essays/costOfChange.htm)

As a DevOps enthusiast I'm interested in ways of failing faster and improving efficiency. A recent example - I like readable code (we all do) by being well formatted (e.g. using the terraform format command). I  often ignore formatting warnings in my editor and forget to execute unit tests for small changes, but it would fail CI. This is waste, we could have failed faster. We should shift further left out of the pipeline and into the IDE so I forced myself to fix errors prior to committing by installing a pre-commit hook - this can also be shared with the team. 

Every-time the pipeline breaks beacuse of a code formatting error, assuming we are following a Trunk-based development approach, someone in the team may have to stop to fix it for them to progress their change, slowing development - this is waste. Should code formatting even fail the build if it functional works?

So what can you do to fail faster and reduce risk:
* Install a pre-commit hook if you forget to validate before committing (e.g. scan for secrets, execute unit tests etc)
* Work to a minimum viable product (MVP) 
* Use metrics and data / feedback to guide solutions
* Execute experiments - Hypothesis Driven Development
* Don't over-optimise, not everything needs to be a "golden" solution - as in my previous blog [post](https://robertnorthard.com/devops-days-well-architected-monoliths-are-okay/) building a "well architected monolith" is more appropriate for eliciting requirements than building a custom micro-service architecture that takes months to fail or deliver value
* Establish CI pipelines from day 1

So when you are working on your next project, going out for dinner without a reservation or taking a car for a MOT ask yourself how can you fail faster!

~ Robert

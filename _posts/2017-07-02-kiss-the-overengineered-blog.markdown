---
title: "Keep it simple stupid - the overengineered blog"
layout: post
date: 2017-07-02 12:48
headerImage: false
tag:
- Cloudflare
- DNS
- KISS
- Overengineered
star: false
category: blog
author: robertnorthard
description: keep it simple stupid - the overengineered blog
---

tldr; simplfying the blog using [Jekyll](https://jekyllrb.com/) and moving to [Cloudflare](https://www.cloudflare.com/ "Cloudflare").

The previous version of this site was composed off a dumb web client (Angular JS), SpringBoot API and a Mongo database all running in Docker (Swarm mode) on a few Raspberry Pis. I only wanted to blog, despite learning a lot this approach had to much operational overhead, so I've simplifed the applications architecture by moving to [Jekyll](https://jekyllrb.com/) and GitHub pages. Jekyll enables you to create a blog from static content. it's easy, plus no more databases to maintain.

# Preivous Blog Architecture

[![Previous Architecture](https://robertnorthard.com/assets/images/2017-07-02-previous_architecture.png "Previous Architecture")](https://robertnorthard.com/assets/images/2017-07-02-previous_architecture.png "Previous Architecture")

# Revised Blog Architecture

[![Revised Architecture](https://robertnorthard.com/assets/images/2017-07-02-revised_architecture.png "Revised Architecture")](https://robertnorthard.com/assets/images/2017-07-02-revised_architecture.png "Revised Architecture")
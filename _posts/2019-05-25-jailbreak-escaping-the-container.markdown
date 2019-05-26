---
title: "#jailbreak - Escaping the container"
layout: post
date: 2019-05-25 15:00
headerImage: false
tag:
- Docker
- Privileged containers
- Root
- jailbreak
star: false
category: blog
author: robertnorthard
description: jailbreak - escaping the container
---

It's common knowledge that Docker containers should not be be run in privileged mode with a shared host PID namespace, but why? In this case a malicious actor, assuming they have access to the container via exec or a vulnerable application, could gain root access to the host using a program like `nsenter`. `nsenter` enables you to execute a process with the context of another processes, for example PID 1.

This example will help provide a concrete example of escaping a container, enabling you to access the hosts file system and execute shell commands.

````

$ docker-machine start default

$ docker run --privileged --rm --pid=host -ti ubuntu 

// This gives you access to the hosts file system
$ nsenter --target 1 --mount sh 

````

This one of many ways you can escape a container. When running containers you will want to drop other [capabilities](http://man7.org/linux/man-pages/man7/capabilities.7.html) such as the ability to reboot a host from inside the container.

~ Robert

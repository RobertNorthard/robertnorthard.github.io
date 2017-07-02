---
title: "Find a Ride"
layout: post
date: 2016-06-17 12:48
headerImage: false
tag:
 - findaride
projects: true
star: false
category: blog
author: robertnorthard
description: Find a Ride
---

<center>
<img src="https://robertnorthard.com/assets/images/2016-06-17-findaride.png" width="250" />
</center>

An Android client and Java server was developed for my final year project as part of my BSc (Hons) Computer Science degree to enable a user to book a taxi and provide real-time updates on the status of the booking and the locations of taxis by integrating with the Google Maps Application Programming Interfaces (APIs). The locations of taxis were simulated.

The server provide RESTful web services for the pull-based interaction between the client and server for the stateless components and WebSockets for streaming taxi location updates events and Google Cloud Messenger (GCM) for pushed-based events such as taxi booking updates.

The server and Android mobile client can be found on GitHub.

[Server Application](https://github.com/RobertNorthard/distributed-taxi-booking-system-server "Server Application")

[Android Mobile App](https://github.com/RobertNorthard/distributed-taxi-booking-system-android-client "Android Mobile App")

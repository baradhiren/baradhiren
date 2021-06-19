---
title: Permission Denied
date: 2021-06-19 09:12:06
tags:
    - Linux
categories: stupid_me
keywords: 
---

# Introduction
This post is about a very simple problem that I came across while leading a task which would improve management's `Visibility` into QA team's efforts and overall software product quality.

# Task
A bit of a background, I was working on integrating a JavaScript based Test Automation Framework with [Reportportal](https://reportportal.io/) to share test results with upper management and also gather insights from our test results on different environments (PR, Staging, Prod, etc... 😄).


# Design
For my Automation Framework to log results to ReportPortal there was a small configuration file that I had to make which looks something like this:

```
"token": "YOUR_RP_TOKEN",
"endpoint": "RP_HOST",
"project": "",
"launch": "",
"description": "Tests"
```

Looks simple. My task would have been done here, If I had to run all tests on every environment from my local.😌 But it doesn't work like that. So, I had to make sure it works on our CI/CD environment as well (Like it should in a normal Software Development team).

# Problem
We have our CI/CD environment built on a cloud computing provider. And the we run our tests on a Dockerized solution using docker-compose files which use Linux as their base OS.

One more thing is before sending data to report portal host we also need to connect to a secure network. And to achieve this we had a small **Shell script** which was doing that for us.

But all my PR builds were failing when it came to running the shell script. And the error it gave was:

```
/code/script.sh: Permission denied
```

# Finding the Root Cause

## First try
My first thought was that my docker-compose context might not be correct and that might have been causing issues. But everything there was alright there so that was not the case.

## Second try
Since context wasn't an issue, I thought Docker container might not have enough permissions. Since I was trying to modify the connection settings of the container, I thought of giving it some extra capabilities using [cap-add](https://docs.docker.com/engine/reference/run/#runtime-privilege-and-linux-capabilities). 

So, I added following things to my docker-compose file:

```
cap_add:
    - NET_ADMIN
devices:
    - /dev/net/tun
```

Still I was getting the same error.
```
/code/script.sh: Permission denied
```

Note: I would have had to add those capabilities later on even if my script started executing. Because without those capabilities docker would not have been able to change the Network Interface and connect to a secure network.

## Third try
After losing all hope and not able to find what the issue is I tried to do one last thing. I tried to run the tests by simulating the cloud environment on my local. Since I use a PC, I built the whole thing and ran tests on my local using Docker and WSL2. And I got the same error. Asking a colleague of mine he casually suggested me if I have assigned execute permissions to the file. 🤦‍♂️
 
Since, I created the file using VS Code on my windows machine it didn't occur to me to assign execute permissions to the file. I gave it execute [privileges](https://www.tutorialspoint.com/unix/unix-file-permission.htm), committed the change and it started working as expected.

I felt so stupid after missing such a basic thing. 😄 

Have you faced any such issues. Connect and let's have a laugh about them on:
- [Twitter](https://twitter.com/baradhiren007) 
- [LinkedIn](https://www.linkedin.com/in/baradhiren)
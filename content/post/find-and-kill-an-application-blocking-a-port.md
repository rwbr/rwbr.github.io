---
title: "Find and Kill an Application Blocking a Port"
date: 2020-10-18T14:57:46+02:00
tags: [os, network]
---

Sometimes when you develop a web application you can run into the problem, that an application is blocking a specific port on your host. This article shows you how to identify that application.

<!--more-->

I recently ran into a situation, where a web application I was working on, blocked a port on my machine. The application ran in background and blocked my desired port. I got the error message:

```
Error: Os { code: 48, kind: AddrInUse, message: "Address already in use" }
```

## What to do

Find the application, that's blocking the port (in my example port **8088**):

```bash
sudo lsof -i :3000
```

Then kill this application:

```bash
kill -9 <PID>
```
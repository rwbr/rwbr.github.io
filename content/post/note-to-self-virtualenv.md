---
title: "Note to self: How to use virtuelenv"
date: 2020-09-04T22:27:47+02:00
---

> virtualenv is a tool to create isolated Python environments. 
> 
What is the basic usage of this command?

<!--more-->

## Installation

```bash
pip3 install virtualenv
```

## Create a virtual envornment

```bash
virtualenv -p python3 <desired-path>
```

## Activate the virtual envornment

```bash
source <desired-path>/bin/activate
```

## Deactivae the virtual envoronment

```bash
deactivate
```

## Remove the virtual environment

```bash
rm -r <desired-path>
```
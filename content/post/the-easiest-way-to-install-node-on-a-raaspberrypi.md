---
title: "The easiest way to install NodeJS on a Raspberry Pi"
date: 2020-08-25T19:29:21+02:00
tags: [nodejs, raspberrypi]
---

The installation of NodeJs on a RaspberryPi can be accomplished on various ways. This article shows the easiest way to do it.

<!--more-->

![Install NodeJS on a RaspberryPi](/img/install-node.jpeg)

## Step 1: Installation of nvm
Use the installation script to install the Node Version Manager:

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.3/install.sh | bash
```

Then the profile script must be executed again (or the terminal restarted):

```bash
source ~/.bashrc
```

Check the nvm version:

```bash
nvm --version
0.35.3
```

## Step 2: Installation of NodeJS

To install a specific NodeJS version using nvm, use the command:

```bash
nvm install <node-version>
```

To set this version as the default version of NodeJS on the system use the command:

```bash
nvm use <node-version>
```

Check the successful installation of the NodeJS version:

```bash
node -v
```

Upgrade from an earlier version:

```bash
nvm install <node-version> —reinstall-packages-from=<old-node-version>
```

Installing NodeJS this way will also install ```npm```.
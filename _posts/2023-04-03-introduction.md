---
layout: post
author: liongrass
tags: [academy]
---

## Welcome to the Node Academy

The Node Academy is an initiative of Vancouver Bitcoiners to grow the number of Lightning Network nodes and increase their quality. It is particularly dedicated to the _Pacific Nodewest_ noderunners community.

The course consists of eight steps and guides the participant from setting up their machine to installing, configuring and maintaining their node. Each step is a guided virtual session in which we explain and discuss the necessary steps and give guidance on how to troubleshoot eventual issues.

### Introduction

In this session we are going through the requirements of running a Lightning Network node, such as access to a physical machine or a virtual private server. If you have not yet made up your mind about where to host your node, this session is a great opportunity to discuss your options and concerns.

The introductory session will also discuss the outline of the course, and give advice on whether you should feel comfortable skipping certain courses or not.

**Objective: Make the decision as to where to run your Lightning Node on**

Absolute minimum requirements:

- 2GB of RAM
- 1 GHz quad core
- 20GB of storage

Suggested requirements:

- 4GB of RAM
- 2 GHz six core
- 256GB SSD

### 1A) Install Ubuntu on a spare computer

Advantages: Self-sovereign solution that maximizes security and affordability.

This session will guide you through the steps necessary to install Ubuntu on a spare laptop or desktop computer of yours. Almost all machines built in the past ten years will be sufficient, and it's up to you to find a suitable machine, either a spare machine you find at home or one you get from a flea market. Check the list above for whether your machine is powerful enough, and don't forget that some parts might be easily upgradable. Either way, you can always upgrade later and move your node to a new device.

Additionally you will need stable internet and electricity where the node is being placed, and it should not pose a fire hazard.

**Objective: Have Ubuntu running on a spare machine at home and being able to SSH into it from your personal computer on the same network**

### 1B) Getting a Virtual Private Server

Advantages: Easy to set up and maintain and build on top of.

Alternative to running our node at home on a spare computer we can also choose to run it in the cloud. This is especially beneficial if you don't have a spare device at home, don't want to buy one or prefer not to have a computer running at home 24/7.

We will discuss various options for a VPS and guide you through the setup process.

**Objective: Have a VPS running that you are able to SSH into from your home network.**

### 2) Introduction to the command line

The command line is a text-based interface in which users can interact with a computer's operating system by typing commands to perform various tasks. We will use it to interact with our node, and while most commands will be explained when they become relevant, this session walks you through the basic tasks, such as creating files, moving or deleting them, navigating your computer's file structure or editing configuration files.

We will also set ourselves up with SSH keys to remotely access our nodes for maintenance.

**Objective: Being able to create, download, move, copy and edit files remotely through the terminal, navigate your machine's file structure and run programs.**

### 3) Install Bitcoin Core

In this step we are going to install Bitcoin Core, configure it and begin the process to sync it to the Blockchain. This syncronization process might take a while, but we will monitor the process before reconvening for part 4.

**Objective: Have Bitcoin Core running and syncing the Bitcoin blockchain.**

### 4) Install LND

In this step we are going to install go, compile and install LND and configure it to connect to Bitcoin Core. We are also going to start LND for the first time to make sure it's working, before completing our course objective in session 5.

Depending on our setup, we are also going to configure our nodes with Tor.

**Objective: Have LND running and syncing to the chain and graph, being able to accept incoming connections over clearnet and/or Tor.**

### 5) Getting started with LND

In this course we are going to complete our course objective, running LND and opening a channel. We are also going to make some test payments to verify that we can both send and receive sats through the Lightning Network.

**Objective: Have LND running with at least one channel, a remote and local balance, make relevant backups and send and receive payments over the Lightning Network.**

### 6) Connect to Zeus, Alby and Lightning Terminal

Additionally, we are going to install litd on top of our node to connect a mobile wallet to our node. We will also learn about the LND Accounts feature that lets us create custodial subaccounts for our friends and family, or connect applications like Alby without giving it the ability to access all our funds. Finally, Lightning Terminal will help us get access to a handy UI and liquidity tools to manage our node.

**Objective: Being able to send and receive payments from Zeus and/or Alby to your own node.**

### 7) Install Thunderhub/RTL/LNbits

- Thunderhub: Thunderhub is a web-based dashboard for managing Lightning Network channels and payments. To install Thunderhub, you can download the latest release from the GitHub repository, install Node.js and Yarn on your system, run the installation script provided, and then start the application using the command line or a process manager like PM2.
- RTL: RTL (Ride The Lightning) is another web-based Lightning Network dashboard that provides a variety of tools for managing channels and payments, including detailed transaction histories and analytics. To install RTL, you can download the latest release from the GitHub repository, install Node.js and NPM on your system, run the installation script provided, and then start the application using the command line or a process manager like PM2.
- LNbits: LNbits is an open-source Lightning Network toolkit that includes a variety of applications and APIs for managing channels, invoices, and more. To install LNbits, you can download the latest release from the GitHub repository, install Python and pipenv on your system, create a new virtual environment, install the required dependencies, and then start the application using the command line. You can also use Docker to run LNbits in a containerized environment.

### 8) Maintain your node

Maintaining a Lightning node involves regularly updating the software to the latest version, monitoring the node's status and channel liquidity, ensuring that backups of critical data are kept, and keeping up to date with the latest security best practices to minimize the risk of potential attacks or data loss.

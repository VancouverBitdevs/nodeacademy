---
layout: post
author: liongrass
tags: [academy, bitcoin]
---

## Installing and syncing Bitcoin Core

Bitcoin Core, also known by its process name `bitcoind`, is by far the most popular implementation of a Bitcoin node. It is written in C++ and as of today available as version 24.0.1. It is a decendant of the "original" Bitcoin implementation, released in January 2009 by Satoshi Nakamoto. The source code can be found on the project's website [bitcoincore.org](https://bitcoincore.org/) as well as the [Github repository.](https://github.com/bitcoin/bitcoin).

### Useful resources:

- [Unix Build Notes](https://github.com/bitcoin/bitcoin/blob/master/doc/build-unix.md)

On Ubuntu, there are three ways we can download the Bitcoin Core software:

- From source, meaning built from the raw source code
- As a binary from the project's website, meaning as a program ready to be executed
- As a binary from a software repository, similar to an app store

Downloading the program from an app store is the most convenient way, but it also requires trust in that app store, as we won't be able to perfectly verify what code we will be running. Downloading the program from the project's site mainly puts trust into the competence of the individuals that compiled the software for us. Compiling from source minimizes trust and (theoretically) allows us to verify line by line what code we will be running on our machine.

As enthusiasts of open source and self-sovereign software, we will recommend installing Bitcoin Core from source, but will also document the other options here for your convenience.

Compiling software can be understood a bit like baking a cake. We take the raw ingrediences, that is math and information, and mix it in a way defined by the recipe, which we download in form of the source code. How exactly we read this recipe depends on the project's programming language.

## From source

This process is the most "raw" of all installation options, and will take a considerable amount of time, possibly over an hour. Whether these steps are purely necessary from a security and sovereignty perspective is debatable, but it's important that we have this option, if we want to verify the code running on our machine, and with it, the Bitcoin blockchain.

### Preparing our machine

To install Bitcoin Core from source, we will first need to install a few software packages that help our system understand the code that we will be compiling. They can be installed in one go with the command below. As part of this command, you will be shown how much space these programs will occupy on your machine. We can agree by typing `Y` and hitting the `Enter` key.

```shell
sudo apt install build-essential libtool autotools-dev automake pkg-config bsdmainutils python3 libevent-dev libboost-dev libsqlite3-dev libzmq3-dev
```

### Downloading the source code

Before we download the source code, we are going to make a new directory that will later contain the source code of all projects we are running on our machine. This will help us stay organized and will make it easier to later maintain our node well.

```shell
mkdir ~/git
cd ~/git
```

Next we are going to download the source code directly from the Github repository.

```
git clone https://github.com/bitcoin/bitcoin.git
cd bitcoin
```

### Compiling Bitcoin Core

Before we compile the software, we will need to specify which version we want to compile. At the time of this writing, the latest version is called `24.1`. You can check the latest version on the [release page of the project](https://github.com/bitcoin/bitcoin/releases).

```shell
git checkout v24.0.1
```

Now we will generate a "makefile". This makefile contains information about our system and its configuration, as well as the limitations and features of our computer. At this step we could theoretically define a long list of potential configuration options, but for the purpose of our node we will stick with the defaults. Be aware that for this command to work, you will need to be in the right directory, which if you followed the steps above, you can always find at `~/git/bitcoin`

```shell
./autogen.sh
./configure
```

Finally we will compile the code. This is going to take a while! If you're unsure about the process, you can always open a new terminal window and run the `top` command to see if a process is taking up our computing power. If it is, then something is hard at work.

```shell
make
```

To install the newly compiled program permanently on our machine, we will install it:

```shell
sudo make install
```

**Congratulations, you now have Bitcoin Core installed on your machine! We can continue to [the next guide](/configure-bitcoin) to configure it.**

## Downloading the binary

Before we begin, for our convenience, we are going to create a separate folder for Downloads. It helps us stay organized and makes it easier to later keep our working directory clean.

```shell
mkdir ~/Downloads
cd ~/Downloads
```

Next we are going to download the correct binary. On the [project's website](https://bitcoincore.org/en/download/) we can find the available software for Windows, Mac OS X and Linux. If you are running your node on a Raspberry Pi, choose the `ARM Linux` link and copy it. All others will use the `Linux (tgz)` link. In Linux, we will download it like this. Replace the filename with your filename if you are using a different version, or a different operating system.

```shell
wget https://bitcoincore.org/bin/bitcoin-core-24.0.1/bitcoin-24.0.1-x86_64-linux-gnu.tar.gz
```

This is a compressed file, similar to a `.zip` file or `.rar` file. We can unpack it with the following command:

```shell
tar xvf bitcoin-24.0.1-x86_64-linux-gnu.tar.gz
```

This will place our binaries into a new folder. We are going to move it somwhere where our system can permanently find it.

```shell
sudo mv bitcoin-24.0.1/bin/* /usr/local/bin/
```

**Congratulations, you now have Bitcoin Core installed on your machine! We can continue to [the next guide](/configure-bitcoin) to configure it.**

## Installing from the Ubuntu Snap Store

Installing Bitcoin Core from the Ubuntu software repository (called the Snap Store) is the most straightforward. To install 

```shell
sudo snap install bitcoin-core
```

By default, Ubuntu will deny programs installed through the Snap Store access to our external drives. If you plan to store the Bitcoin blockchain on drive other than your main drive, you will need to permit access with:

```shell
sudo snap connect bitcoin-core:removable-media
```

**Congratulations, you now have Bitcoin Core installed on your machine! We can continue to [the next guide](/configure-bitcoin) to configure it.**

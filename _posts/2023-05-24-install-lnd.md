---
layout: post
author: liongrass
tags: [academy, lnd]
---

## Installing LND

The Lightning Network Daemon (LND) is a Lightning Network node implementation written in go. It is by far the most popular routing node on the Lightning Network today. You can find it's source code at [github.com/lightningnetwork/lnd](https://github.com/lightningnetwork/lnd).

Litd is a software bundle that includes LND, as well as Lightning Lab's Lightning Network tools [Loop](https://docs.lightning.engineering/lightning-network-tools/loop), [Pool](https://docs.lightning.engineering/lightning-network-tools/pool), [Faraday](https://docs.lightning.engineering/lightning-network-tools/faraday) and [Taproot Assets](https://docs.lightning.engineering/lightning-network-tools/taproot-assets). Through `litd` we can access other useful features such as [LND Accounts](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/accounts), [Lightning Node Connect](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/lightning-node-connect) and [Lightning Terminal](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/connect).

In this section, we are going to install the `litd` software bundle to give us easy access to all of the features we need without going through multiple installations. Litd is fully open-source.

### Useful resources:

- [Litd Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/run-litd)
- [LND Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lnd/run-lnd)

Similar to Bitcoin Core, there are two ways we can download litd:

- From source, meaning built from the raw source code
- As a binary from the project's website, meaning as a program ready to be executed

Downloading the binary from the project's repository would again be the most convenient, but we will nonetheless compile it from source for maximum verifiability and accountability.

## From source

Unlike with Bitcoin Core, we will not need to install many dependencies, and the compilation process will be much quicker. But we will need to install the programming language golang, as it does not come bundled with Ubuntu by default.

### Install dependencies

We will need to install [nodejs and yarn](https://nodejs.org/en/download/).

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 22
```

We can then verify that nodejs is installed by running:

```shell
node -v
```

Which should show something like: `v22.19.0`
Enabling yarn is then as easy as:

```shell
corepack enable yarn
```

You can verify yarn is installed by running:

```shell
yarn -v
```

The first time you do that, you will be asked to confirm the download. Enter `Y` and press `Enter` to continue.

### Install/Upgrade go

If Go is already installed and needs to be upgraded, do this procedure to find out installation folder, make sure the path on the third like matches the output of which go command.

```shell
go version

which go

sudo rm -rf /usr/local/go
```

We can find the latest version of go on its [official website](https://go.dev/dl/). At the time of writing, this is `go1.25.1`. We open a terminal on our Ubuntu machine or SSH into it and download the golang source code.

```shell
cd ~/Downloads
wget https://go.dev/dl/go1.25.1.linux-amd64.tar.gz
```
Note: if ~/Downloads folder does not exist on your machine create a folder and try again
```shell
mkdir ~/Downloads
```

We are now going to unpack this repository with the command:

```shell
sudo tar -C /usr/local -xzf go1.25.1.linux-amd64.tar.gz
```

Next we will have to make sure our machine learns about where to find the golang code, and where to place programs that we will install with go. To do that, we are going to edit the `.bashrc` file.

```shell
nano ~/.bashrc
```

At the very bottom, we will place the following snippet:

```
### GOLANG
export PATH=$PATH:/usr/local/go/bin
export GOPATH=~/go
export PATH=$PATH:$GOPATH/bin
```

We will once again save our edits with `Ctrl` + `O` and `Enter`, then exit the editor with `Ctrl` + `X`.


We can now check our installation.

```shell
bash
```
```shell
go version
```

The output should read: `go version go1.25.1 linux/amd64`

### Downloading the source code

We'll once again enter our git directory, where we download our source code.

```shell
cd ~/git
```

Next we are going to download the source code for litd directly from the Github repository.

```shell
git clone https://github.com/lightninglabs/lightning-terminal.git
cd lightning-terminal
```

### Compiling litd

Before we compile the software, we will need to specify which version we want to compile. At the time of this writing, the latest version is called `0.15.2`. You can check the latest version on the [release page of the project](https://github.com/lightninglabs/lightning-terminal/releases).

```shell
git checkout v0.15.2-alpha
```

We can now install the software with

```shell
make install
make go-install-cli
```

We can verify that `litd` is properly installed on our machine with:

```shell
litd --version
```

It should output `litd version 0.15.2-alpha commit=v0.15.2-alpha commit_hash=911f8cae52670332fe46affd35ff18458ebd5ffb`.

**Congratulations, you now have LND, Pool, Loop, Faraday and litd installed on your machine! We can continue to [the next guide](/configure-lnd) to configure it.**

## Downloading the binary

We once again navigate to our downloads folder, which should already exist on our machine.

```shell
cd ~/Downloads
```

Next we are going to download the correct binary. On the [project's website](https://github.com/lightninglabs/lightning-terminal/releases) we can find the available software for Windows, Mac OS X and Linux. If you are running your node on a Raspberry Pi, choose the `ARM Linux` link and copy it. Most others will use the `linux-amd64[...].tar.gz` link. In Linux, we will download it like this. Replace the filename with your filename if you are using a different version, or a different operating system.

```shell
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz
```

This is a compressed file, similar to a `.zip` file or `.rar` file. We can unpack it with the following command:

```shell
tar xvf lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz
```

As we don't want to blindly trust the binaries being legit, we are going to verify them using GPG. To do that, we are going to add the GPG keys of the maintainer. We only have to do this once, as we upgrade later we will no longer have to download the key.

```shell
gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys C20A78516A0944900EBFCA29961CC8259AE675D4
```

Next, we are going to download the manifest and the signature and check whether the manifest is properly signed.

```shell
cd ~/Downloads
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/manifest-v0.15.2-alpha.txt
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/manifest-ViktorT-11-v0.15.2-alpha.sig
gpg --verify manifest-ViktorT-11-v0.15.2-alpha.sig manifest-v0.15.2-alpha.txt
```

We should get the result: `gpg: Good signature from "Viktor Torstensson <viktor.t.git@gmail.com>"`

Finally, we will have to check whether the SHA256 hash of the binaries we downloaded matches what is signed in the manifest.

```shell
cd ~/Downloads
sha256sum -c --ignore-missing manifest-v0.15.2-alpha.txt
```

You should see `OK` printed behind every file:

```shell
lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/frcli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/litcli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/litd: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/lncli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/loop: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/pool: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/tapcli: OK
```

Now we will place our binaries into a new folder. We are going to move it somewhere where our system can permanently find it.

```shell
sudo mv lightning-terminal-linux-amd64-v0.15.2-alpha/* /usr/local/bin/
```

We can verify that `litd` is properly installed on our machine with:

```shell
litd --version
```

It should output `litd version 0.15.2-alpha commit=v0.15.2-alpha commit_hash=911f8cae52670332fe46affd35ff18458ebd5ffb`.

**Congratulations, you now have LND, Pool, Loop, Faraday and litd installed on your machine! We can continue to [the next guide](/configure-lnd) to configure it.**

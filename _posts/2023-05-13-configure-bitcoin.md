---
layout: post
author: liongrass
tags: [academy, bitcoin]
---

## Configuring Bitcoin Core

Before we start Bitcoin Core for the first time, we are going to configure it with the minimal settings. We are going to add other configuration options later as we need them.

First, we are going to create a configuration file and place it in the directory where Bitcoin Core can find it as we start it up.

### Useful resources:

- [Jameson Lopp's Bitcoin config file generator](https://jlopp.github.io/bitcoin-core-config-generator/)
- [Complete sample bitcoin.conf file](/bitcoin-conf)

### Create a configuration file

If you installed Bitcoin Core from source or downloaded the binaries, make a folder called `.bitcoin` in your home directory, then open a text editor to place the config file here.

```shell
mkdir ~/.bitcoin
nano ~/.bitcoin/bitcoin.conf
```

If you installed Ubuntu from the Ubuntu Snap Store, you can directly edit the configuration file with:

```shell
nano ~/snap/bitcoin-core/common/.bitcoin/bitcoin.conf
```

We can use the following sample configuration file, adjust it to our needs and paste it into the editor. Lines that begin with a pound sign (`#`) represent comments and will not be read by Bitcoin Core. They exist to maximize our understanding of what each line does and how we can configure it. Feel free to remove these comments, or add your own.

```
# The directory we want to use to store the blockchain. If you are using a single drive, remove this setting. Otherwise, specify the path of your external drive.
datadir=/mnt/bitcoin

# We prune the blockchain to 40GB so that it fits on our 50GB drive.
# The other 10GB will be free to be taken by other data of Bitcoin Core, such as the UTXO set.
prune=40000
```

We can now save this file (`Ctrl` + `O`) + (`Enter`) to confirm filename and exit (`Ctrl` + `X`) the editor.

### Start Bitcoin Core

To start Bitcoin Core, we use the command:

```shell
bitcoind --daemon
```

We should see the message: `Bitcoin Core starting`.

If you installed Bitcoin Core from the Ubuntu Snap Store, the correct command to start the program is:

```shell
bitcoin-core.daemon --daemon
```

### Obsere the logs

We can now follow the log files with this command. Adjust the path if your bitcoin directory is elsewhere:

```
tail -f /mnt/bitcoin/debug.log
```

We can exit this log by pressing `Ctrl` + `C`.

You may exit the terminal now at any time by typing `exit`. Bitcoin Core should keep running as long as the computer is not turned off. You should be able to check on your progress anytime by logging into yor machine and following the logs as above.

Your logs will likely show mostly lines like the onese below as it is syncing. The **progress** variable shows your approximate progress in percent, while the **date** shows the day on which the block was mined that your node just synchronized. The **height** variable shows the block height. You will notice that syncing through the first five to seven years of Bitcoin is relatively quick, while the past five years will take relatively long.

```
2023-05-14T06:49:49Z UpdateTip: new best=00000000078cd7fe612131d19e796bfdad7afd22b1002bf2ff2a801f519a7bef height=35236 version=0x00000001 log2_work=47.131723 tx=35468 date='2010-01-18T16:49:53Z' progress=0.000043 cache=7.6MiB(35403txo)
```

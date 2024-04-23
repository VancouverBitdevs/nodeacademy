---
layout: post
author: liongrass
tags: [academy, lnd]
---

## Configure LND

Before we start LND for the first time, we are going to configure it with the minimal settings. This is also the time we will need to amend some settings to Bitcoin Core!

First, we are going to create a configuration file and place it in the directory where Bitcoin Core can find it as we start it up.

### Useful resources:

- [Litd Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/run-litd)
- [LND Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lnd/run-lnd)
- [Lastpass Password generator tool](https://www.lastpass.com/features/password-generator#generatorTool)
- [LND sample configuration file](/lnd-conf)

### Configure Bitcoin Core

Our Bitcoin Core configuration file should be in their default position. We can open it with the following command:

```shell
nano ~/.bitcoin/bitcoin.conf
```

We will mainly have to amend two settings. One allows LND to connect to Bitcoin Core remotely, for example to look up blocks, transactions and publish channel openings. The other allows LND to subscribe to new blocks and transactions without having to specifically query for them.

Before you paste the below into your configuration file, generate a user and password using a random number generation tool, such as your local password manager. You can also use an online tool such as [Lastpass](https://www.lastpass.com/features/password-generator#generatorTool). Then replace the user and password with your own.

```
# Enabling remote procedure calls
rpcuser=dontusethis
rpcpassword=makeyourownpassword

# Enabling ZMQ
zmqpubrawblock=tcp://127.0.0.1:28332
zmqpubrawtx=tcp://127.0.0.1:28333
```

### Configure LND

First we will make a folder for the configuration file, then we can edit it with the text editor.

```shell
mkdir ~/.lit
nano ~/.lit/lit.conf
```

Here's a sample configuration file that you can use. Don't forget to edit

- Your node's alias (optional)
- Your node's color (optional)
- The uipassword
- The Bitcoin RPC username and password (must match what you entered into your `bitcoin.conf`)

```
# Basic Configuration
uipassword=dontusethisyouwillgethacked
lnd-mode=integrated

# Node alias
lnd.alias=nodeacademy
lnd.color=#FF0000

# Bitcoin Core Options
lnd.bitcoin.mainnet=1
lnd.bitcoin.node=bitcoind
lnd.bitcoind.rpchost=127.0.0.1
lnd.bitcoind.rpcuser=dontusethis
lnd.bitcoind.rpcpass=makeyourownpassword
lnd.bitcoind.zmqpubrawblock=tcp://127.0.0.1:28332
lnd.bitcoind.zmqpubrawtx=tcp://127.0.0.1:28333
```

## Test LND

We can test our installation and connection with the command:

```shell
litd
```

If it doesn't stop or crash with an error, great! **We've completed our configuration process!**

You can stop the process by pressing `Ctrl` + `C`. That should send the shutdown signal and `litd` should shut down gracefully.

### Optional: Listen for incoming connections on clearnet (recommended for nodes with a static IP)

If you're running your node on clearnet and have a static IP address, you can listen for incoming connections on that IP address. You can also advertise an IPv4 and IPv6 address at the same time. Be aware of the privacy implications! In case you are running your node at home or an office, making it available over its clearnet IP might make the node's location know to a sophisticated attacker.

To advertise our IP address, we simply add the following to our `lit.conf` file. Don't forget to replace the values in externalip with your own! If your node does not have a IPv4 or IPv6 address, simply leave out that line.

```
lnd.listen=0.0.0.0:9735
lnd.externalip=2602:ffb6:4:c927:f816:3eff:fea0:ef40
lnd.externalip=172.81.179.14
```

We will once again start `litd` to test our configuration:

```shell
litd
```

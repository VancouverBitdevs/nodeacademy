---
layout: post
author: liongrass
tags: [academy, lnd]
---

## Install Tor

Tor is a public relay network that helps us to both anonymize our node's location, as well as be able to accept incoming connections through a "Tor Hidden Service." Even if our node is running on clearnet, installing Tor is often useful, as it allows to reach Tor-only nodes and make ourselves available through a hidden service, which can make connections to Tor nodes more reliable.

### Useful resources:

- [Tor Project on Github](https://github.com/torproject/tor)
- [Tor Project Support](https://support.torproject.org/)

## Install Tor from the repository (recommended)

You can install tor from the Ubuntu software repository with the command:

```shell
sudo apt install tor
```

**Congratulations, you have installed Tor! [Skip ahead to see how to configure Tor and LND](#configure-tor)**


## Install Tor from source

You may install Tor from source using the instructions below.

### Prepare our machine

We will have to install some packages on our machine so we can compile Tor.

```shell
sudo apt install automake libevent-dev libssl-dev zlib1g zlib1g-dev asciidoc
```

### Download and compile Tor

We will once again compile Tor from source. We will enter our git directory and clone the source code from there.

```shell
cd ~/git
git clone https://git.torproject.org/tor.git
cd tor
```

We will compile the code by executing the commands below, one by one. Look out for eventual error messages!

```shell
./autogen.sh
./configure
make
sudo make install
```

You can now run tor with `tor`, but the application will quit when you close the terminal. To push the process into the background run:

`nohup tor > /dev/null 2> /home/ubuntu/tor_err.log &`

**Congratulations, you have installed Tor! Continue below to configure Tor and LND](#configure-lnd)**

## Configure Tor

To make use of Tor with LND, we best give LND access to the Tor daemon and handle all the details itself. For that we will need to generate another password. Use your password manager and retain it until you are done this guide. You won't have to record this password or retain it after this configuration.

```shell
tor --hash-password dontusethisyouwillbehacked
```

Using your own password above, you should get an output like this:

```
16:1394205CE9C9256460207A14A8C90FF867FA3B5C6EC2A2054615D71871
```

Now we will edit the tor configuration file. You can find it like this:

```shell
sudo nano /etc/tor/torrc
```

Find the section that starts with `#HashedControlPassword` and enter in a new line below. Don't forget to replace the hash with your personal hash as obtained above!

```
HashedControlPassword 16:1394205CE9C9256460207A14A8C90FF867FA3B5C6EC2A2054615D71871
```

Additionally, we will have to find the line that reads `#ControlPort 9051` and remove the pound sign so it reads:

```
ControlPort 9051
```

We now save and close the editor and restart Tor with the command:

```shell
sudo service tor restart
```

## Configure LND

We will mainly have to again amend settings. This will set LND to listen to incoming connections, activate tor and tell it how to connect and authenticate to Tor.

```shell
nano ~/.lit/lit.conf
```

We will enter the following lines:

```
# Tor configuration
lnd.listen=0.0.0.0:9735
lnd.tor.active=true
lnd.tor.socks=127.0.0.1:9050
lnd.tor.control=localhost:9051
lnd.tor.password=dontusethisyouwillbehacked
lnd.tor.v3=true
```

Optionally, we may also add the following line. Only add this line if you are also operating on clearnet, or if you are comfortable revealing your home IP address to your clearnet peers.

```
lnd.tor.skip-proxy-for-clearnet-targets=1
```

We will save and exist the editor.

## Test LND

We can test our installation and connection with the command:

```shell
litd
```

If it doesn't stop or crash with an error, great! **We've completed our Tor configuration process!**

You can stop the process by pressing `Ctrl` + `C`. That should send the shutdown signal and `litd` should shut down gracefully.

## Configure Bitcoin Core (optional)

We can also configure Bitcoin Core to connect to its peers over the Tor network.

All we'll have to do is add the following line to our configuration file in `~/.bitcoin/bitcoin.conf`.

```
proxy=127.0.0.1:9050
```

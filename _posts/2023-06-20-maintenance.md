---
layout: post
author: liongrass
tags: [academy, linux]
---

## Linux

This week we are going to perform some basic maintenance on our nodes. We are also going to register both bitcoin and LND with systemd, allowing us to set everything to start automatically when the machine starts.

### Useful resources:

- [Upgrading LND](https://docs.lightning.engineering/lightning-network-tools/lnd/run-lnd#docs-internal-guid-277e81aa-7fff-ccda-4359-bf5ca2a712bc)

### Update the operating system

Applying all recent updates is easy. We only need to run the following two commands consecutively and type `Y` then prompted:

```shell
sudo apt update
sudo apt upgrade
```

Depending on what kind of updates we are getting we might have to confirm a few other prompts. Going with the defaults is generally fine for our purpose, so pressing the `Enter` key is enough.

Occasionally our machine will ask us to restart it. This is not urgent, but can be done with the command:

```shell
sudo reboot now
```

It might be wise to shut down LND and Bitcoin Core before you do that!


### Upgrade Bitcoin Core

To upgrade Bitcoin Core, we will first have to enter the directory where we keep the source code, then pull the latest code from the repository.

```shell
cd ~/git/bitcoin
git pull
```

As a reponse, you should immediately see which _tags_ have been added since you last pulled code from this repository.

```
 * [new tag]             v22-final  -> v22-final
 * [new tag]             v23.2      -> v23.2
 * [new tag]             v24.1      -> v24.1
 * [new tag]             v25.0      -> v25.0
```

This tells us that since we last visited the code, there are new versions available. We are going to go forward with upgrading to `v25.0`

```shell
git checkout v25.0
```

You might see an error like `error: Your local changes to the following files would be overwritten by checkout:`. In this case, you can stash all changes with:

```shell
git stash
```

We can try `git checkout v25.0` again and should see something like the following:

```
Previous HEAD position was b3f866a8d Merge bitcoin/bitcoin#26647: 24.0.1 final changes
HEAD is now at 8105bce5b Merge bitcoin/bitcoin#27686: 25.0 Final Changes
```

As we have built Bitcoin on this machine before, we are going to install it simply with:

```shell
make
sudo make install
```

We will now stop Bitcoin Core and start it again, then check if we are on the correct version.

```shell
bitcoin-cli stop
bitcoind --daemon
bitcoin-cli --getinfo
```

We should see the version now at v25.0: `Version: 250000`

### Upgrade LND

To upgrade LND, we are going to navigate to our `lightning-terminal` directory, and similar to the above, we are going to pull the latest code, checkout the latest version and build it.

```shell
cd ~/git/lightning-terminal
git pull
git checkout v0.10.1-alpha
make go-install go-install-cli
```

We can now start LND again, unlock it and check the versioning.

```shell
nohup litd &
lncli unlock
litcli ---version
```

You should see `litcli version 0.10.1-alpha commit=v0.10.1-alpha` as the output. Success!

### Register Bitcoin Core with systemd

Systemd is a Linux tool that allows us to simplify starting and stopping programs. We can register Bitcoin Core with systemd, allowing us to start and stop it with a simpler command, and configure it to start automatically at startup.

First we are going to stop Bitcoin Core.

```shell
bitcoin-cli stop
```

Now we are going to create the necessary directories and assign them to the Ubuntu user that we are running with.

```shell
sudo mkdir /run/bitcoind
sudo chown ubuntu:ubuntu /run/bitcoind
```

Next we are going to create the service file, also called the Unit File. This file contains information for the system on where to run a program, how to run it, and when to run it.

```shell
sudo nano /etc/systemd/system/bitcoind.service
```

Past the following into the editor:

```
[Unit]
Description=Bitcoin daemon
Documentation=https://github.com/bitcoin/bitcoin/blob/master/doc/init.md

# https://www.freedesktop.org/wiki/Software/systemd/NetworkTarget/
After=network-online.target
Wants=network-online.target

[Service]
ExecStart=/usr/local/bin/bitcoind -daemonwait \
                            -pid=/run/bitcoind/bitcoind.pid \
                            -conf=/home/ubuntu/.bitcoin/bitcoin.conf

# Process management
####################

Type=forking
PIDFile=/run/bitcoind/bitcoind.pid
Restart=on-failure
TimeoutStartSec=infinity
TimeoutStopSec=600

# Directory creation and permissions
####################################

# Run as ubuntu:ubuntu
User=ubuntu
Group=ubuntu

# /run/bitcoind
RuntimeDirectory=bitcoind
RuntimeDirectoryMode=0710


# Hardening measures
####################

# Provide a private /tmp and /var/tmp.
PrivateTmp=true

# Disallow the process and all of its children to gain
# new privileges through execve().
NoNewPrivileges=true

# Use a new /dev namespace only populated with API pseudo devices
# such as /dev/null, /dev/zero and /dev/random.
PrivateDevices=true

# Deny the creation of writable and executable memory mappings.
MemoryDenyWriteExecute=true

[Install]
WantedBy=multi-user.target
```

We can save the editor with `Ctrl` + `O` and exit with `Ctrl` + `X`.

To activate this file, we run:

```shell
sudo systemctl enable --now bitcoind.service
```

You will have to exist this window with `Ctrl` + `C` after reading `Created symlink /etc/systemd/system/multi-user.target.wants/bitcoind.service → /etc/systemd/system/bitcoind.service.`

We can now check if the service is running properly.

```shell
systemctl status bitcoind.service
```

![Bitcoin Daemon](/images/bitcoind.png)

Most importantly we should see `Active: active (running)`. We can exit this view with `Ctrl` + `C` and check the logs.

```shell
journalctl -u bitcoind.service
```

You can exit these logs with `Ctrl` + `C` and then `Enter`. We can also try to restart our machine with `sudo reboot now` and then check if Bitcoin Core is automatically running.

In the future, if we need to stop Bitcoin Core manually we can do that with:

```shell
sudo systemctl stop bitcoind.service
```

And stop it again with:

```shell
sudo systemctl start bitcoind.service
```

**Congratulations, Bitcoin Core now starts automatically after each restart.**

### Register LND with systemd

We can also configure LND (or litd) to start automatically when we reboot our machine. We have the option here to also configure LND to automatically unlock, but this will require us to keep the wallet password file on the same device, rather than in a password manager. If you are not comfortable doing that, you can skip straight to creating the unit file, but you will have to manually unlock LND everytime you start up the machine with `lncli unlock`.

In this example, we are placing the LND password into the `.lnd` directory, but you may put it into the `.lit` directory instead too.

```shell
nano ~/.lnd/password
```

Enter your password into this document in the first line, and nothing else. Then save and close with `Ctrl` + `O` and `Ctrl` + `X`.

Next we are going to let our litd installation know about the existence of this file by pointing to it in the configuration file.

```shell
nano ~/.lit/lit.conf
```

And place the following line into it before saving and exiting:


```
lnd.wallet-unlock-password-file=/home/ubuntu/.lnd/password
```

Next we are creating the unit file, similar to how we created the Bitcoin Core unit file:

```shell
sudo nano /etc/systemd/system/litd.service
```

The unit file can be found below:

```
[Unit]
Description=Litd daemon

After=bitcoind.service
Wants=bitcoind.service

[Service]
ExecStart=/home/ubuntu/go/bin/litd

# Process management
####################

PIDFile=/run/bitcoind/litd.pid
Type=simple
KillMode=process
TimeoutSec=180
Restart=always
RestartSec=60

# Directory creation and permissions
####################################

# Run as ubuntu:ubuntu
User=ubuntu
Group=ubuntu

# Hardening measures
####################

# Provide a private /tmp and /var/tmp.
PrivateTmp=true

# Disallow the process and all of its children to gain
# new privileges through execve().
NoNewPrivileges=true

# Use a new /dev namespace only populated with API pseudo devices
# such as /dev/null, /dev/zero and /dev/random.
PrivateDevices=true

# Deny the creation of writable and executable memory mappings.
MemoryDenyWriteExecute=true

[Install]
WantedBy=multi-user.target
```

Next we are going to enable this service.

```
sudo systemctl enable --now litd.service
```

We should see the output `Created symlink /etc/systemd/system/multi-user.target.wants/litd.service → /etc/systemd/system/litd.service.`

We can now check if litd is running with:

```shell
systemctl status litd.service
```

The service log file can be found with:

```shell
journalctl -u litd.service
```

**Awesome, litd is configured to automatically start whenever you reboot the machine. Try it out!**

In the future, if we need to stop LND manually we can do that with:

```shell
sudo systemctl stop litd.service
```

And stop it again with:

```shell
sudo systemctl start litd.service
```

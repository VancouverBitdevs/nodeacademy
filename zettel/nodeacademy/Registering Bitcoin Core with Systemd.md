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

Most importantly we should see `Active: active (running)`. We can exit this view with `Ctrl` + `C` and check the logs.

```shell
journalctl -u bitcoind.service
```

You can exit these logs with `Ctrl` + `C` and then `Enter`. We can also try to restart our machine with `sudo reboot now` and then check if Bitcoin Core is automatically running.

In the future, if we need to stop Bitcoin Core manually we can do that with:

```shell
sudo systemctl stop bitcoind.service
```

And start it again with:

```shell
sudo systemctl start bitcoind.service
```

**Congratulations, Bitcoin Core now starts automatically after each restart.**

[[Installing LND from Source]]
[[Installing LND from the Binaries]]

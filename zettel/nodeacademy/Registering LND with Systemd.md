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

And start it again with:

```shell
sudo systemctl start litd.service
```

[[Installing LND from Source]]
[[Installing LND from the Binaries]]

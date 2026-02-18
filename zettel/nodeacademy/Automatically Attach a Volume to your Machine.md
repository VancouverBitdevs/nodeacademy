To make sure our server automatically mounts this volume when we start it, we are going to have to edit some configuration files.

First, we will find out the UUID of our SSD by running the following. If we can't see our drive, we have to reboot the machine with `sudo reboot now`, then reconnect via SSH:

```shell
lsblk -f
```

Typically, the last line will show the mounted bitcoin disk. Look for `vdc` under NAME and `/mnt/bitcoin` under MOUNTPOINTS. A typical UUID looks like this: `50fb9f4-60e7-4024-adde-2a9959214dd6`.

Next, we are going to open the nano editor and edit the `fstab` file:

```shell
sudo nano /etc/fstab
```

We are going to paste (right-click and paste or if your computer/mouse has one, the middle button) the following line:

`UUID=<your SSD's UUID> <your mount path> ext4 defaults 0 0`

For example:

`UUID=050fb9f4-60e7-4024-adde-2a9959214dd6 /mnt/bitcoin ext4 defaults 0 0`

Now are going to save the file with `Ctrl` + `O` and exit the editor with `Ctrl` + `X`.

We are going to test our configuration by mounting all the volumes.

```shell
sudo systemctl daemon-reload
sudo mount -a
```

If this succeeds without error, we can optionally reboot our server.

```shell
sudo reboot now
```

We will have to wait a minute for our server to reboot before we can log back in with SSH.

```shell
df -h
```

We should see something like the following.

```
Filesystem      Size  Used Avail Use% Mounted on
tmpfs            98M  996K   97M   2% /run
/dev/vda1        16G  2.0G   14G  13% /
tmpfs           486M     0  486M   0% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
/dev/vdc        4.9G   24K   80G   0% /mnt/bitcoin
/dev/vda15      105M  5.3M  100M   5% /boot/efi
tmpfs            98M  4.0K   98M   1% /run/user/1000
```

[[Format a volume]]
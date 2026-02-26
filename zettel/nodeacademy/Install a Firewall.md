The Uncomplicated Firewall (UFW) should already be installed on your Ubuntu system. You can check with the command:

```shell
sudo ufw status
```

It should return something like `Status: inactive`. Otherwise you can install it with:

```shell
sudo apt install ufw
```

Before we enable the firewall, we are going to have to allow SSH connections into our machine, or else we might find ourselves locked out. If you are not using SSH to monitor or control your computer, for example because your computer has a keyboard and monitor attached to it, we don't need to enable SSH.

```shell
sudo ufw allow ssh
```

It should return `Rules updated`.

Next, we are going to enable our firewall:

```shell
sudo ufw enable
```

We confirm with `y` and should see the notice: `Firewall is active and enabled on system startup`

**Important:** Before we continue, keep the existing terminal open and start a new terminal window and try to SSH into your machine. If this does not succeed, disable the firewall before trying the `sudo ufw allow ssh` command again:

```shell
sudo ufw disable
```

[[Connect to your node]]

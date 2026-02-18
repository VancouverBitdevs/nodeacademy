We will also set ourselves up with SSH keys to remotely access our nodes for maintenance.

In this step, we are going to get ready to access our device from our personal computer via SSH. To do that, we are going to first create an SSH key. We recommend you creating a new SSH key, in case you will later need to revoke it or exchange it.

#### Create an SSH key on your personal machine

In Mac OS X, Windows or Linux we are going to open a terminal for the first time and execute the following.

```shell
ssh-keygen
```

We are typically asked for a name for this key, for example `nodekey_rsa`. You may optionally choose a passphrase for this key, meaning you will have to enter this passphrase every time you log into your machine. Your public key will be called `newkey_rsa.pub` and it will be saved in the following location:

Windows: `C:\Documents and Settings\userName\Application Data\SSH\UserKeys\newkey_rsa.pub`
Linux: `~/.ssh/newkey_rsa.pub`
Mac OS: `/Users/MYUSERNAME/.ssh/newkey_rsa.pub`

Save this file on a USB stick, we are going to carry it over to our node later.

[[Installing Ubuntu]]
[[Provision a Virtual Private Server on Lunanode]]

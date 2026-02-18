You can check the status of your firewall.

```shell
sudo ufw status
```

It should return `Status: active` and a list of existing rules.

We are going to add a rule that lets us connect to the user interface of litd. As we only very rarely need access to this interface, I would recommend to change the rules when you need access, then pull the firewall back up once you're done.

```shell
sudo ufw allow 8443
```

We will also make sure that the following line is added to our `lit.conf` file: `httpslisten=0.0.0.0:8443`

```shell
nano ~/.lit/lit.conf
```

If you have to add this line, don't forget to restart LND and unlock it!

```shell
lncli stop
nohup litd > /dev/null 2> ~/.lnd/err.log &
lncli unlock
```

[[Install a Firewall]]

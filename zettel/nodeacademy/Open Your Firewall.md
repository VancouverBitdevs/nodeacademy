Depending on what services you make use of on your machine, you may want to open other ports too. Generally, you should only do this if your node is running on a clearnet IP address.

Incoming connections to LND:

```shell
sudo ufw allow 9735
```

Incoming connections to Bitcoin Core:

```shell
sudo ufw allow 8333
```

[[Install a Firewall]]
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

[[Configure LND]]
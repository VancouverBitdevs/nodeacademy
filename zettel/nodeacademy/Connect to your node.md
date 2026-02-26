On your personal computer, open a terminal window and connect via the following command:

```shell
ssh <username>@<ip address>
```

More specifically, this may look like this:

```shell
ssh ubuntu@192.168.1.110
```

If you are running into errors, you may have to specify the location and name of the SSH key you want to use:

```shell
ssh -i ~/.ssh/id_rsa <username>@<ip address>
```

For instance, if you did not name your key `id_rsa`, substitute its name in the command above. If the key is located elsewhere, specify it's path as shown above.


As this is your first time connecting to the node, you will see a warning "the authenticity of the host can not be established" together with the SSH fingerprint of your node. You can type `yes` to add this fingerprint to your configuration, and you will only receive a warning in the future if the fingerprint does not match.

### SSH Troubleshooting

- SSH settings
- Firewall: Ubuntu uses "ufw" (uncomplicated firewall). It is disabled by default but if you are interested in using it [more information can be found here](https://ubuntu.com/server/docs/security-firewall)
- Ping the node using `ping <ip address>`

[[Obtain your IP on a Spare Computer]]
[[Obtain your IP on Lunanode]]

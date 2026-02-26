Lightning Node Connect is a convenient tool to connect your node to Zeus and Alby, or to manage your node using Lightning Terminal. It excels especially in comparison to connections over Tor.

If your node is available over a clearnet IP, then connecting directly from Zeus may provide a significantly superior experience.

### Get your macaroon

We'll need our node's macaroon. You can for example use the admin macaroon from LND and print it in hex.

`xxd -p -c 256 ~/.lnd/data/chain/bitcoin/mainnet/admin.macaroon | tr -d '\n'`

If you would like to make a custodial sub account with a 1 satoshi balance, you may this command:

`litcli accounts create 1 --save_to ~/zeus.macaroon`

Then print it in hex format:

`xxd -p -c 256 ~/zeus.macaroon | tr -d '\n'`

It is also possible to create a macaroon for an existing LND Account. [Follow this guide if you want to do that](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/accounts#docs-internal-guid-d0641bc1-7fff-0871-8cd4-de3e495890fc)

### Open your firewall

To be able to receive connections over the REST interface, we will need to open port 8080 on our node.

`sudo ufw allow 8080`

### Update lit.conf to listen on port 8080

Update lit.conf to be able to listen to rest interface on port 8080

```shell
nano ~/.lit/lit.conf
```
Use the arrow keys to navigate to the end of the file then add

`lnd.restlisten=0.0.0.0:8080`

Press CRTL-O to save and CTRL-X to exit

Restart litd service by typing 
```shell
sudo systemctl restart litd.service
```

### Connect Zeus

In Zeus, go into settings, then click on your existing node name, then on the big `+` symbol on the top right.

Give your node a nickname, choose `LND (REST)` as the node interface.

Your host is your IP address.

Under "macaroon", enter your macaroon in hex format as obtained in the step above.

Under "REST port", enter `8080`.

Leave 'Use Tor' and Certificate verification `unchecked` and click save node config

You should be able to save your node configuration and connect right away.

[[Run LND]]

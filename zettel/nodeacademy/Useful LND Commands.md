Get basic information about your active daemon, such as if it's running, synced to the main chain, your node URI, etc.

```shell
lncli getinfo
```

Generates a new onchain Taproot address for your node. You can use it to deposit funds to your node.

```shell
lncli newaddress p2tr
```

Shows your on-chain balance:

```shell
lncli walletbalance
```

Opens a channel. Don't forget to substitute nodekey and the node's URI! You can find ranked nodes to open channels to on [LightningTerminal](https://terminal.lightning.engineering/).

```shell
lncli openchannel --node_key <nodekey> --connect <ip address or onion>:<port> --local_amt 2200000 --sat_per_vbyte 2
```

You can see whether a channel is currently opening or closing with:

```shell
lncli pendingchannels
```

You can see all your channels with:

```shell
lncli listchannels
```

You can pay an invoice with:

```shell
lncli payinvoice <invoice>
```

You can make an onchain payment with:

```shell
lncli sendcoins
```

You can see if your node forwarded any payments with:

```shell
lncli fwdinghistory
```

You can sign a message with:

```shell
lncli signmessage
```

You can see all available commands with:

```shell
lncli help
```

You can turn off LND with:

```shell
lncli stop
```

[[Run LND]]

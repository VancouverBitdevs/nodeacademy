The Lightning Network Daemon (LND) is a Lightning Network node implementation written in go. It is by far the most popular routing node on the Lightning Network today. You can find it's source code at [github.com/lightningnetwork/lnd](https://github.com/lightningnetwork/lnd).

Litd is a software bundle that includes LND, as well as Lightning Lab's Lightning Network tools [Loop](https://docs.lightning.engineering/lightning-network-tools/loop), [Pool](https://docs.lightning.engineering/lightning-network-tools/pool), [Faraday](https://docs.lightning.engineering/lightning-network-tools/faraday) and [Taproot Assets](https://docs.lightning.engineering/lightning-network-tools/taproot-assets). Through `litd` we can access other useful features such as [LND Accounts](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/accounts), [Lightning Node Connect](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/lightning-node-connect) and [Lightning Terminal](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/connect).

In this section, we are going to install the `litd` software bundle to give us easy access to all of the features we need without going through multiple installations. Litd is fully open-source.

### Useful resources:

- [Litd Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lightning-terminal/run-litd)
- [LND Installation Guide](https://docs.lightning.engineering/lightning-network-tools/lnd/run-lnd)

Similar to Bitcoin Core, there are two ways we can download litd:

- From source, meaning built from the raw source code
- As a binary from the project's website, meaning as a program ready to be executed

Downloading the binary from the project's repository would again be the most convenient, but we will nonetheless compile it from source for maximum verifiability and accountability.

[[Bitcoin Core Logs]]

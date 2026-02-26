Most likely, our LND logs will eventually stop at the following line:

```
2023-06-06 15:10:05.825 [INF] LTND: Version: 0.16.2-beta commit=v0.16.2-beta, build=production, logging=default, debuglevel=info
2023-06-06 15:10:05.825 [INF] LTND: Active chain: Bitcoin (network=mainnet)
2023-06-06 15:10:05.825 [INF] RPCS: Generating TLS certificates...
2023-06-06 15:10:05.828 [INF] RPCS: Done generating TLS certificates
2023-06-06 15:10:05.831 [INF] RPCS: RPC server listening on 127.0.0.1:10009
2023-06-06 15:10:05.834 [INF] RPCS: gRPC proxy started at 127.0.0.1:8080
2023-06-06 15:10:05.834 [INF] LTND: Opening the main database, this might take a few minutes...
2023-06-06 15:10:05.834 [INF] LTND: Opening bbolt database, sync_freelist=false, auto_compact=false
2023-06-06 15:10:06.889 [INF] LTND: Creating local graph and channel state DB instances
2023-06-06 15:10:09.757 [INF] CHDB: Checking for schema update: latest_version=29, db_version=29
2023-06-06 15:10:09.757 [INF] CHDB: Checking for optional update: prune_revocation_log=false, db_version=empty
2023-06-06 15:10:09.757 [INF] LTND: Database(s) now open (time_to_open=3.923391736s)!
2023-06-06 15:10:09.758 [INF] LTND: We're not running within systemd or the service type is not 'notify'
2023-06-06 15:10:09.758 [INF] LTND: Waiting for wallet encryption password. Use `lncli create` to create a wallet, `lncli unlock` to unlock an existing wallet, or `lncli changepassword` to change the password of an existing wallet and unlock it.
```

As this is our first time opening LND, we will generate a new wallet. Ideally, use the second Terminal window and run

```shell
lncli create
```

At first, we will be asked for a wallet password. Choose a good password, ideally from your password manager. You will have to enter it everytime you start up LND.

```
Do you have an existing cipher seed mnemonic or extended master root key you want to use?
Enter 'y' to use an existing cipher seed mnemonic, 'x' to use an extended master root key 
or 'n' to create a new seed (Enter y/x/n):
```

Next, we are asked if we already have a seed. Unless we are restoring an old, **inactive** node, we will generate a new seed by pressing `n`.

Optionally, you are asked if you want to encrypt your seed phrase. If you opt to do so, don't forget to back up this encryption phrase, too! Otherwise, just leave the field empty and press `Enter`.

Write down the seed phrase, in your password manager or ideally on a piece of paper and store it well. You are not able to retrieve the seed phrase later from your node.

Your node will now begin to sync to the Blockchain, and then to the network graph.

```
2025-09-18 15:13:18.964 [INF] LNWL: Started rescan from block 00000000000000000002e56ebe6959efb73a3c09fd177c1f5a9041a103b6657f (height 792856) for 0 addresses
2025-09-18 15:15:03.275 [INF] LNWL: Catching up block hashes to height 793172, this might take a while
2025-09-18 15:15:03.277 [INF] LNWL: Done catching up block hashes
2025-09-18 15:15:03.278 [INF] LNWL: Finished rescan for 0 addresses (synced to block 000000000000000000055507311aafceeb734d5ab028c9ca24750c32ddf7af91, height 793172)
2025-09-18 15:15:03.918 [INF] LTND: Chain backend is fully synced (end_height=793172)!
2025-09-18 15:15:03.919 [WRN] HLCK: check: disk space configured with 0 attempts, skipping it
2025-09-18 15:15:03.919 [WRN] HLCK: check: tls configured with 0 attempts, skipping it
2025-09-18 15:15:03.919 [INF] LNWL: SigPool starting
2025-09-18 15:15:03.961 [INF] CHNF: ChannelNotifier starting
2025-09-18 15:15:03.961 [INF] PRNF: PeerNotifier starting
2025-09-18 15:15:03.961 [INF] HSWC: HtlcNotifier starting
2025-09-18 15:15:03.961 [INF] SWPR: Sweeper starting
2025-09-18 15:15:03.961 [INF] BTCN: Broadcaster now active
2025-09-18 15:15:03.961 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.961 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.961 [INF] UTXN: UTXO nursery starting
2025-09-18 15:15:03.968 [INF] BRAR: Breach arbiter starting
2025-09-18 15:15:03.969 [INF] FNDG: Funding manager starting
2025-09-18 15:15:03.969 [INF] HSWC: HTLC Switch starting
2025-09-18 15:15:03.969 [INF] BRAR: Starting contract observer, watching for breaches.
2025-09-18 15:15:03.968 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.996 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.996 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.996 [INF] CNCT: ChainArbitrator starting
2025-09-18 15:15:03.996 [INF] DISC: Authenticated Gossiper starting
2025-09-18 15:15:03.996 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:03.996 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:04.005 [INF] CRTR: Channel Router starting
2025-09-18 15:15:04.031 [INF] CRTR: FilteredChainView starting
2025-09-18 15:15:04.066 [INF] CRTR: Filtering chain using 0 channels active
2025-09-18 15:15:04.081 [INF] CRTR: Prune tip for Channel Graph: height=793172, hash=000000000000000000055507311aafceeb734d5ab028c9ca24750c32ddf7af91
2025-09-18 15:15:04.093 [INF] INVC: InvoiceRegistry starting
2025-09-18 15:15:04.094 [INF] HSWC: Onion processor starting
2025-09-18 15:15:04.094 [INF] NTFN: New block epoch subscription
2025-09-18 15:15:04.119 [INF] NANN: Channel Status Manager starting
2025-09-18 15:15:04.119 [INF] CHFT: ChannelEventStore starting
2025-09-18 15:15:04.119 [INF] CHFT: Adding 0 channels to event store
2025-09-18 15:15:04.119 [INF] CHBU: chanbackup.SubSwapper starting
2025-09-18 15:15:04.119 [INF] NTFN: New block epoch subscription
```

This shouldn't take very long as we only just generated our wallet, and LND will only need to scan through the most recent blocks to see if we already made an on-chain transaction to our node.

Next our node is going to sync to the network graph, meaning it is going to download a list of all Lightning Network channels in existence.

```
2025-09-18 15:16:08.868 [INF] SRVR: Initializing peer network bootstrappers!
2025-09-18 15:16:08.868 [INF] SRVR: Creating DNS peer bootstrapper with seeds: [[nodes.lightning.directory soa.nodes.lightning.directory] [lseed.bitcoinstats.com ]]
2025-09-18 15:16:08.868 [INF] DISC: Attempting to bootstrap with: Authenticated Channel Graph
2025-09-18 15:16:08.873 [INF] DISC: Attempting to bootstrap with: BOLT-0010 DNS Seed: [[nodes.lightning.directory soa.nodes.lightning.directory] [lseed.bitcoinstats.com ]]
```

We can always follow the progress.

```shell
lncli getinfo
```

We'll be looking for the following lines in the output to tell us when we are fully synced to the network graph:

```
    "synced_to_chain": true,
    "synced_to_graph": true
```

You can also run this command to see progress:

```shell
lncli getnetworkinfo
```

For a fully synced node, it will look something like this. Note that no two Lightning Nodes are exactly the same, they will always have a slightly different view of the network based on how old they are, how they are configured and where in the graph they are located.

```
{
    "graph_diameter":  14,
    "avg_out_degree":  3.892202121023082,
    "max_out_degree":  111,
    "num_nodes":  16030,
    "num_channels":  31196,
    "total_network_capacity":  "135989999541",
    "avg_channel_size":  4359212.704866009,
    "min_channel_size":  "1050",
    "max_channel_size":  "500000000",
    "median_channel_size_sat":  "1000000",
    "num_zombie_chans":  "364355"
}
```


[[Useful LND Commands]]
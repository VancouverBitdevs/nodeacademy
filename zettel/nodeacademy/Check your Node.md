As we SSH into our server, we are first going to make sure everything is running smoothly. 

```shell
lncli getinfo
```

The part of the output we're looking for tells us that we are synced to the blockchain and the network graph.

```
    "synced_to_chain": true,
    "synced_to_graph": true,
```

[[Useful LND Commands]]

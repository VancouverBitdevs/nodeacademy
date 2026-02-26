We're looking for the `uri` output of `lncli getinfo`. Your node may have more than one URI, but it should have at least one to be reachable from the outside. It is also possible to run a node without it being reachable from the outside, but this makes having incoming channels more complicated. Below is an example of a node with an IPv6, IPv4 and Tor URI.

```
    "uris": [
        "03bcc5841bb86378fdec070cb53edff7a40c49ceb401fc3c0b5696a35b9c34433f@[2602:ffb6:4:c927:f816:3eff:fefa:fd70]:9735",
        "03bcc5841bb86378fdec070cb53edff7a40c49ceb401fc3c0b5696a35b9c34433f@172.81.178.0:9735",
        "03bcc5841bb86378fdec070cb53edff7a40c49ceb401fc3c0b5696a35b9c34433f@qzqmq4gmgmpqa7yb5ktof2zvdycvmcglk3mrxp7mdsofolckygeyytyd.onion:9735"
    ]
```


[[Useful LND Commands]]
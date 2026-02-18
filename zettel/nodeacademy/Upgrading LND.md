To upgrade LND, we are going to navigate to our `lightning-terminal` directory, and similar to the above, we are going to pull the latest code, checkout the latest version and build it.

```shell
cd ~/git/lightning-terminal
git pull
git checkout v0.15.2-alpha
make go-install go-install-cli
```

We can now start LND again, unlock it and check the versioning.

```shell
nohup litd > /dev/null 2> ~/.lnd/err.log &
lncli unlock
litd --version
```

You should see `litd version 0.15.2-alpha commit=v0.15.2-alpha commit_hash=911f8cae52670332fe46affd35ff18458ebd5ffb` as the output. Success!

[[Installing LND from Source]]
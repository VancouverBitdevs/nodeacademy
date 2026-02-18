To upgrade Bitcoin Core, we will first have to enter the directory where we keep the source code, then pull the latest code from the repository.

```shell
cd ~/git/bitcoin
git pull
```

As a response, you should immediately see which _tags_ have been added since you last pulled code from this repository.

```
   837c5c7fd8..7e1eca4882  29.x       -> origin/29.x
 * [new branch]            30.x       -> origin/30.x
   f5f853d952..edb871cba2  master     -> origin/master
 * [new tag]               v29.2rc1   -> v29.2rc1
 * [new tag]               v29.1      -> v29.1
 * [new tag]               v29.1rc2   -> v29.1rc2
 * [new tag]               v30.0rc1   -> v30.0rc1
```

This tells us that since we last visited the code, there are new versions available. We are going to go forward with upgrading to `v25.0`

```shell
git checkout v29.1
```

You might see an error like `error: Your local changes to the following files would be overwritten by checkout:`. In this case, you can stash all changes with:

```shell
git stash
```

We can try `git checkout v29.1` again and should see something like the following:

```
Previous HEAD position was b3f866a8d Merge bitcoin/bitcoin#26647: 24.0.1 final changes
HEAD is now at 8105bce5b Merge bitcoin/bitcoin#27686: 25.0 Final Changes
```

As we have built Bitcoin on this machine before, we are going to install it simply with:

```shell
cmake -B build -DWITH_ZMQ=ON
cmake --build build 
sudo cmake --install build
```

We will now stop Bitcoin Core and start it again, then check if we are on the correct version.

```shell
bitcoin-cli stop
bitcoind --daemon
bitcoin-cli --getinfo
```

We should see the version now at v29.1: `Version: 290000`

[[Installing Bitcoin Core From Source]]

Before we start Bitcoin Core for the first time, we are going to configure it with the minimal settings. We are going to add other configuration options later as we need them.

First, we are going to create a configuration file and place it in the directory where Bitcoin Core can find it as we start it up.

If you installed Bitcoin Core from source or downloaded the binaries, make a folder called `.bitcoin` in your home directory, then open a text editor to place the config file here.

```shell
mkdir ~/.bitcoin
nano ~/.bitcoin/bitcoin.conf
```

If you installed Ubuntu from the Ubuntu Snap Store, you can directly edit the configuration file with:

```shell
nano ~/snap/bitcoin-core/common/.bitcoin/bitcoin.conf
```

We can use the following sample configuration file, adjust it to our needs and paste it into the editor. Lines that begin with a pound sign (`#`) represent comments and will not be read by Bitcoin Core. They exist to maximize our understanding of what each line does and how we can configure it. Feel free to remove these comments, or add your own.

```
# The directory we want to use to store the blockchain. If you are using a single drive, remove this setting. Otherwise, specify the path of your external drive.
datadir=/mnt/bitcoin

# We prune the blockchain to 40GB so that it fits on our 50GB drive.
# The other 10GB will be free to be taken by other data of Bitcoin Core, such as the UTXO set.
prune=40000
```

We can now save this file (`Ctrl` + `O`) + (`Enter`) to confirm filename and exit (`Ctrl` + `X`) the editor.


[[Installing Bitcoin Core From Source]]
[[Installing Bitcoin Core from the Binaries]]
[[Installing Bitcoin Core from the Snap Store]]
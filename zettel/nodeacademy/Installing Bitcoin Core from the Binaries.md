Before we begin, for our convenience, we are going to create a separate folder for Downloads. It helps us stay organized and makes it easier to later keep our working directory clean.

```shell
mkdir ~/Downloads
cd ~/Downloads
```

Next we are going to download the correct binary. On the [project's website](https://bitcoincore.org/en/download/) we can find the available software for Windows, Mac OS X and Linux. If you are running your node on a Raspberry Pi, choose the `ARM Linux` link and copy it. All others will use the `Linux (tgz)` link. In Linux, we will download it like this. Replace the filename with your filename if you are using a different version, or a different operating system.

```shell
wget https://bitcoincore.org/bin/bitcoin-core-29.0/bitcoin-29.0-x86_64-linux-gnu.tar.gz
```

This is a compressed file, similar to a `.zip` file or `.rar` file. We can unpack it with the following command:

```shell
tar xvf bitcoin-29.0-x86_64-linux-gnu.tar.gz
```

This will place our binaries into a new folder. We are going to move it somwhere where our system can permanently find it.

```shell
sudo mv bitcoin-29.0/bin/* /usr/local/bin/
```
[[Installing Bitcoin Core]]

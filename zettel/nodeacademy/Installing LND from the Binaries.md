We once again navigate to our downloads folder, which should already exist on our machine.

```shell
cd ~/Downloads
```

Next we are going to download the correct binary. On the [project's website](https://github.com/lightninglabs/lightning-terminal/releases) we can find the available software for Windows, Mac OS X and Linux. If you are running your node on a Raspberry Pi, choose the `ARM Linux` link and copy it. Most others will use the `linux-amd64[...].tar.gz` link. In Linux, we will download it like this. Replace the filename with your filename if you are using a different version, or a different operating system.

```shell
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz
```

This is a compressed file, similar to a `.zip` file or `.rar` file. We can unpack it with the following command:

```shell
tar xvf lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz
```

As we don't want to blindly trust the binaries being legit, we are going to verify them using GPG. To do that, we are going to add the GPG keys of the maintainer. We only have to do this once, as we upgrade later we will no longer have to download the key.

```shell
gpg --keyserver hkps://keyserver.ubuntu.com --recv-keys 187F6ADD93AE3B0CF335AA6AB984570980684DCC
```

Next, we are going to download the manifest and the signature and check whether the manifest is properly signed.

```shell
cd ~/Downloads
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/manifest-v0.15.2-alpha.txt
wget https://github.com/lightninglabs/lightning-terminal/releases/download/v0.15.2-alpha/manifest-ViktorTigerstrom-v0.15.2-alpha.sig
gpg --verify manifest-ViktorTigerstrom-v0.15.2-alpha.sig manifest-v0.15.2-alpha.txt
```

We should get the result: `gpg: Good signature from "Viktor Tigerström <vtigerstrom@gmail.com>"`

Finally, we will have to check whether the SHA256 hash of the binaries we downloaded matches what is signed in the manifest.

```shell
cd ~/Downloads
echo "$(cat manifest-v0.15.2-alpha.txt) lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz" | sha256sum -c --ignore-missing
```

You should see `OK` printed behind every file:

```shell
lightning-terminal-linux-amd64-v0.15.2-alpha.tar.gz: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/frcli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/litcli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/litd: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/lncli: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/loop: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/pool: OK
lightning-terminal-linux-amd64-v0.15.2-alpha/tapcli: OK
```

Now we will place our binaries into a new folder. We are going to move it somewhere where our system can permanently find it.

```shell
sudo mv lightning-terminal-linux-amd64-v0.15.2-alpha/* /usr/local/bin/
```

We can verify that `litd` is properly installed on our machine with:

```shell
litd --version
```

It should output `litd version 0.15.2-alpha commit=v0.15.2-alpha commit_hash=911f8cae52670332fe46affd35ff18458ebd5ffb`.

[[Installing LND]]

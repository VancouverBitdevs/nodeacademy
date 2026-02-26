We'll once again enter our git directory, where we download our source code.

```shell
cd ~/git
```

Next we are going to download the source code for litd directly from the Github repository.

```
git clone https://github.com/lightninglabs/lightning-terminal.git
cd lightning-terminal
```

### Compiling litd

Before we compile the software, we will need to specify which version we want to compile. At the time of this writing, the latest version is called `0.13.1`. You can check the latest version on the [release page of the project](https://github.com/lightninglabs/lightning-terminal/releases).

```shell
git checkout v0.15.2-alpha
```

We can now install the software with

```shell
make install
make go-install-cli
```

We can verify that `litd` is properly installed on our machine with:

```shell
litd --version
```

It should output `litd version 0.15.2-alpha commit=v0.15.2-alpha commit_hash=911f8cae52670332fe46affd35ff18458ebd5ffb`.

[[Installing Go]]

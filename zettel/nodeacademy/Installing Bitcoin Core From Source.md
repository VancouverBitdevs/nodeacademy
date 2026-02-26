This process is the most "raw" of all installation options, and will take a considerable amount of time, possibly over an hour. Whether these steps are purely necessary from a security and sovereignty perspective is debatable, but it's important that we have this option, if we want to verify the code running on our machine, and with it, the Bitcoin blockchain.

### Requirements

To install Bitcoin Core from source, we will first need to install a few software packages that help our system understand the code that we will be compiling. They can be installed in one go with the command below. As part of this command, you will be shown how much space these programs will occupy on your machine. We can agree by typing `Y` and hitting the `Enter` key.

```shell
sudo snap install cmake --classic
sudo apt install build-essential cmake pkgconf python3 libevent-dev libboost-dev libsqlite3-dev libzmq3-dev
```

### Downloading the source code

Before we download the source code, we are going to make a new directory that will later contain the source code of all projects we are running on our machine. This will help us stay organized and will make it easier to later maintain our node well.

```shell
mkdir ~/git
cd ~/git
```

Next we are going to download the source code directly from the Github repository.

```
git clone https://github.com/bitcoin/bitcoin.git
cd bitcoin
```

### Compiling Bitcoin Core

Before we compile the software, we will need to specify which version we want to compile. At the time of this writing, the latest version is called `27`. You can check the latest version on the [release page of the project](https://github.com/bitcoin/bitcoin/releases).

```shell
git checkout v29.0
```

Now we will generate a "makefile". This makefile contains information about our system and its configuration, as well as the limitations and features of our computer. At this step we could theoretically define a long list of potential configuration options, but for the purpose of our node we will stick with the defaults. Be aware that for this command to work, you will need to be in the right directory, which if you followed the steps above, you can always find at `~/git/bitcoin`. The `DWITH_ZMQ=ON` flag will make sure ZMQ is compiled, as we will need it later.

```shell
cmake -B build -DWITH_ZMQ=ON
```

Finally we will compile the code. This is going to take a while! If you're unsure about the process, you can always open a new terminal window and run the `top` command to see if a process is taking up our computing power. If it is, then something is hard at work.

```shell
cmake --build build 
```

To install the newly compiled program permanently on our machine, we will install it:

```shell
sudo cmake --install build
```

You can now verify you installed the correct version:

```shell
bitcoind --version
```

You should see: `Bitcoin Core daemon version v29.0`


[[Installing Bitcoin Core]]

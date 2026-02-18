If Go is already installed and needs to be upgraded, do this procedure to find out installation folder, make sure the path on the third like matches the output of which go command.

```shell
go version

which go

sudo rm -rf /usr/local/go
```

We can find the latest version of go on its [official website](https://go.dev/dl/). At the time of writing, this is `go1.22.5`. We open a terminal on our Ubuntu machine or SSH into it and download the golang source code.

```shell
cd ~/Downloads
wget https://go.dev/dl/go1.25.1.linux-amd64.tar.gz
```
Note: if ~/Downloads folder does not exist on your machine create a folder and try again
```shell
mkdir ~/Downloads
```

We are now going to unpack this repository with the command:

```shell
sudo tar -C /usr/local -xzf go1.25.1.linux-amd64.tar.gz
```

Next we will have to make sure our machine learns about where to find the golang code, and where to place programs that we will install with go. To do that, we are going to edit the `.bashrc` file.

```shell
nano ~/.bashrc
```

At the very bottom, we will place the following snippet:

```
### GOLANG
export PATH=$PATH:/usr/local/go/bin
export GOPATH=~/go
export PATH=$PATH:$GOPATH/bin
```

We will once again save our edits with `Ctrl` + `O` and `Enter`, then exit the editor with `Ctrl` + `X`.


We can now check our installation.

```shell
bash
go version
```

The output should read: `go version go1.25.1 linux/amd64`

[[Installing LND from Source (Dependencies)]]

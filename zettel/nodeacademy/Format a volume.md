We will log back into our node via SSH from our personal computer.

We can execute the following command to check if our volume is successfully attached:

```shell
lsblk
```

Typically, we will find it at the very bottom labelled `vdc`. The main storage partition of our server is likely called `vda`. You should be able to see their sizes too.

Next, we are going to format this SSD. We type and execute:

```shell
sudo mkfs.ext4 /dev/vdc
```

Depending on the size of your volume, this can be very fast or take a minute.

Now, we are going to permanently mount this volume. First we are going to create a directory called `bitcoin`.

```shell
sudo mkdir /mnt/bitcoin
```

Next, we are going to mount the drive at this directory.

```shell
sudo mount /dev/vdc /mnt/bitcoin
```

We can see a list of all mounted volumes with the `df` utility.

```shell
df -h
```

Finally, we are going to give permission over this new volume back to the user ubuntu, as it is initially owned by the root user.

```shell
sudo chown ubuntu:ubuntu /mnt/bitcoin
```

[[Create a Volume in Lunanode]]
Installing Bitcoin Core from the Ubuntu software repository (called the Snap Store) is the most straightforward. To install 

```shell
sudo snap install bitcoin-core
```

By default, Ubuntu will deny programs installed through the Snap Store access to our external drives. If you plan to store the Bitcoin blockchain on drive other than your main drive, you will need to permit access with:

```shell
sudo snap connect bitcoin-core:removable-media
```

[[Installing Bitcoin Core]]
LNbits regularly releases new updates with patches and new features. To update, first navigate to where you downloaded the LNbits source code.

```shell
cd ~/git/lnbits
```

We will get the latest code and checkout the latest version. Observe the output of the `git checkout` command to see which versions are new!

```shell
git pull
git checkout 1.2.1
```

First we will update poetry before we update lnbits itself.

```shell
poetry self update
poetry install --only main
```
Finally, we will have to restart LNbits, assuming we have set up systemd as explained above.

```shell
sudo systemctl restart lnbits.service
```

You should now be able to navigate to your LNbits installation and confirm you are running the installed version at the bottom of the screen.

[[Install LNbits]]

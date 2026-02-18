First we will need to make sure the SSH server is installed. On our node, we are going to open a terminal and type:

```shell
sudo apt update
sudo apt install openssh-server
```

Next, we will need need to authorize our new SSH key to access the node. We can do this with the command line, or in the graphical user interface.

**Command line:**

Open a terminal and edit the `authorized_keys` file. If the file is not there, this command will also create it.

```shell
nano ~/.ssh/authorized_keys
```

We will paste our SSH key from the step above into this file into line one. It will look like this

`ssh-rsa AAAAB3NzaC1yc2EAAAADAQABAAABgQD5GTA4m8[...]M810pRF88pgY255H/KUmL77PHiMTom+1n2Levmi6M0= user@device`

We will save this file by pressing `Ctrl` + `O` and `Enter` and exit the application with `Ctrl` + `X`.

**Graphical interface:**

Open the files explorer (called Nautilus or Files), typically found on the top left of the screen, or by searching for Files.

By default you should be in your _Home_ folder. To display hidden folders, press `Ctrl` + `H` on your keyboard, you should see a folder named `.ssh`.

Now we plug our USB with the ssh into our node, rename the public key `newkey_rsa.pub` to `authorized_keys` (without a dot or file extension in the end), and place it into the `.ssh` folder.

[[Generate SSH Keys]]

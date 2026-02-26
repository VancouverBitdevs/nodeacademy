We assume you already have your Lightning node as set up through the Nodeacademy guides.

We'll prepare our server by installing the required dependencies. Most of them should already be present if you followed these guides.

```shell
sudo apt install -y build-essential pkg-config libffi-dev libpq-dev zlib1g-dev libssl-dev python3-dev libsqlite3-dev ncurses-dev libbz2-dev libreadline-dev lzma-dev liblzma-dev
```

Next we are going to install pyenv

```shell
curl https://pyenv.run | bash
```

Once the script finishes running, you should see a Warning that you still haven't added `pyenv` to your load path. You should be given a command like:

```
export PYENV_ROOT="$HOME/.pyenv"
[[ -d $PYENV_ROOT/bin ]] && export PATH="$PYENV_ROOT/bin:$PATH"
eval "$(pyenv init - bash)"
```

Copy these lines and open `~/.profile` using `nano ~/.profile`. Go to the very bottom and paste it there, then save and close the editor.
Repeat for `~/.bashrc`

Now exit your Terminal by typing `exit` and log back into your server.

We can now run `pyenv init`

Next we will install python 3.10 with the command:

```shell
pyenv install 3.10.4
```

We wiil now install poetry:

```
curl -sSL https://install.python-poetry.org | python3 - --version 1.8.5
echo export PATH=\"$HOME/.local/bin:$PATH\" >> ~/.bashrc
source ~/.bashrc
```

[[Run LND]]

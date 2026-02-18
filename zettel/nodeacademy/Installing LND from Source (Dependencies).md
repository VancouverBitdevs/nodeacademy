Unlike with Bitcoin Core, we will not need to install many dependencies, and the compilation process will be much quicker. But we will need to install the programming language golang, as it does not come bundled with Ubuntu by default.
### Install dependencies

We will need to install [nodejs and yarn](https://nodejs.org/en/download/).

```shell
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.40.3/install.sh | bash
\. "$HOME/.nvm/nvm.sh"
nvm install 22
```

We can then verify that nodejs is installed by running:

```shell
node -v
```

Which should show something like: `v22.19.0`
Enabling yarn is then as easy as:

```shell
corepack enable yarn
```

You can verify yarn is installed by running:

```shell
yarn -v
```

The first time you do that, you will be asked to confirm the download. Enter `Y` and press `Enter` to continue.

[[Installing LND]]


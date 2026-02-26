Prerequisites

To make use of LNbits, your server needs to be accessible through an IP address (ideally both IPv4 and IPv6). You will also need a domain name. If you already have a domain name but use it for something else such as your website, you should be able to create a subdomain free of charge and point it at your LNbits installation.

If you don't have a domain name and always wanted one, you can buy domains with [Namecheap](https://www.namecheap.com/) with sats. I use [Cloudflare](https://www.cloudflare.com/) for free DNS.

Furthermore, we need to download some additional software:

```shell
sudo apt install python3.12-dev pkg-config libffi-dev libpq-dev
curl -sSL https://install.python-poetry.org | python3 -
export PATH="$HOME/.local/bin:$PATH"
```

(Depending on your setup, the last command might look slightly different. The output of the previous command should give you the correct example.)

### Download LNbits

We will navigate to our git directory and clone the LNbits repository.

```shell
cd ~/git
git clone https://github.com/lnbits/lnbits.git
cd lnbits
git checkout <latest version, e.g. v1.2.1>
```

### Configure LNbits

We configure LNbits by first creating a data directory, then copying and editing the default configuration file.

```shell
cp .env.example .env
nano .env
```

Next we will have to find and amend the following four lines in this file:

```
LNBITS_BACKEND_WALLET_CLASS=LndRestWallet
LND_REST_CERT="/home/ubuntu/.lnd/tls.cert"
LND_REST_MACAROON="/home/ubuntu/.lnd/data/chain/bitcoin/mainnet/admin.macaroon"
```

### Install LNbits

Next, we are going to install LNbits

```shell
poetry env use python3.12
poetry install --only main
```

[[LNbits]]

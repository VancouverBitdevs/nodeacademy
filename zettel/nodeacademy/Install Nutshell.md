
We can now proceed with the installation of the mint itself. Find out which version was released most recently by going to [the projects github page](https://github.com/cashubtc/nutshell/releases).

```shell
cd git
git clone https://github.com/cashubtc/nutshell.git
cd nutshell
git checkout <latest_tag>
pyenv local 3.10.4
poetry install
```

#### Configuration

We are going to first copy the configuration file.

```shell
cp .env.example .env
```

The following lines are relevant:

`MINT_PRIVATE_KEY=`
Generate a private key using the command `openssl rand -hex 32` and enter it here. Don't forget to remove the `#` sign at the beginning of the line.

`MINT_BACKEND_BOLT11_SAT=`
Your best option is likely `LndRestWallet`, unless you also have [LNbits](/lnbits) installed, in which case `LNbitsWallet` may be more practical.

```
MINT_LND_REST_ENDPOINT=https://127.0.0.1:8086
MINT_LND_REST_CERT="/home/ubuntu/.lnd/tls.cert"
MINT_LND_REST_MACAROON="/home/ubuntu/.lnd/data/chain/bitcoin/regtest/admin.macaroon
```

Or if you choose to connect to LNbits, enter your LNbits endpoint and the admin key of a new blank wallet here:

```
MINT_LNBITS_ENDPOINT=https://legend.lnbits.com
MINT_LNBITS_KEY=yourkeyasdasdasd
```

[[Nutshell Prerequisites]]
[[LNbits]]

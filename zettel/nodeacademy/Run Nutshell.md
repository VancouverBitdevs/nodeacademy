In our `~/git/nutshell` directory, we can now run nutshell with:

```shell
poetry env activate
poetry run mint
```

Keep your mint running in this stage, and continue in a new terminal window. We will later configure the mint to run automatically on startup.

#### Additional configuration

Optionally, you can also point a new domain name at your VPS, define a name for your Mint, add a description, contact email, add a message to the users or even add terms of service.

### Make your mint publicly accessible 

We are going to use Caddy as a reverse proxy. You might already have it installed when you configured LNbits.

```shell
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

Next, stop caddy and edit the configuration file, which may already exist on your system.

```shell
sudo caddy stop
sudo nano /etc/caddy/Caddyfile
```

At the very bottom, at this to your file. Don't forget to replace your domain name.

```
ecash.nodeacademy.org {
	reverse_proxy 127.0.0.1:3338 {
		header_up X-Forwarded-Host ecash.nodeacademy.org
	}
}
```

Then start caddy:

`sudo caddy start --config /etc/caddy/Caddyfile`

You should now be able to add your mint to your ecash wallet.

[[Install Nutshell]]

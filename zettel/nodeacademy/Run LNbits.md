We can run LNbits for the first time using simply:

`poetry run lnbits`

This should give us an indication of whether LNbits is properly set up. We can stop LNbits with `Ctrl` + `C`, but for now, we'll keep it running, and instead open a new terminal shell.

### Install the reverse proxy

We are going to use Caddy as the reverse proxy. If you're experienced in configuring Apache or Nginx, you may also use those. You can find some [additional guides here](https://github.com/lnbits/lnbits/blob/main/docs/guide/installation.md).

```shell
sudo apt install -y debian-keyring debian-archive-keyring apt-transport-https
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/gpg.key' | sudo gpg --dearmor -o /usr/share/keyrings/caddy-stable-archive-keyring.gpg
curl -1sLf 'https://dl.cloudsmith.io/public/caddy/stable/debian.deb.txt' | sudo tee /etc/apt/sources.list.d/caddy-stable.list
sudo apt update
sudo apt install caddy
```

As caddy is now installed, it is also running already! We will have to stop caddy to change its configuration.

```shell
sudo caddy stop
sudo nano /etc/caddy/Caddyfile
```

We can use the following configuration file. Make sure to replace `lnbits.nodeacademy.org` with your own domain name!

```
lnbits.nodeacademy.org {
	handle /api/v1/payments/sse* {
		reverse_proxy 0.0.0.0:5000 {
			header_up X-Forwarded-Host lnbits.nodeacdemy.org
			transport http {
				keepalive off
				compression off
			}
		}
	}
	reverse_proxy 0.0.0.0:5000 {
		header_up X-Forwarded-Host lnbits.nodeacademy.org
	}
}
```

Next, we will have to point the DNS records of this domain to our IP address. We can find our IP address in the admin panel of our VPS provider, e.g. Lunanode.

In our example, the records are `172.81.178.0` (IPv4) and `2602:ffb6:4:c927:f816:3eff:fefa:fd70` (IPv6).

We will point the A (IPv4) and AAAA (IPv6) records of our domain to this IP address. Check with your domain registrar or DNS provider.

Finally, we are going to start caddy. We have to make sure to be in the right directory when we do that!

```shell
`sudo caddy start --config /etc/caddy/Caddyfile`
```

If we have configured a firewall (UFW), then we also have to open ports 80 and 443!

```shell
sudo ufw allow http
sudo ufw allow https
```

[[Install LNbits]]

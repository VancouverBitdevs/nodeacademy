
Next we will make sure nutshell starts up automatically when you reboot your machine.

We will create a systemd file.

`sudo nano /etc/systemd/system/nutshell.service`

We can paste the following:

```
# Systemd unit for lnbits
# /etc/systemd/system/nutshell.service

[Unit]
Description=Nutshell
# you can uncomment these lines if you know what you're doing
# it will make sure that nutshell starts after litd (replace with your own backend service)
Wants=litd.service
After=litd.service

[Service]
# replace with the absolute path of your nutshell installation
WorkingDirectory=/home/ubuntu/git/nutshell
# same here. run `which poetry` if you can't find the poetry binary
ExecStart=/home/ubuntu/.local/bin/poetry run mint
# replace with the user that you're running nutshell on
User=ubuntu
Restart=always
TimeoutSec=120
RestartSec=30
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
```

We can then activate the file with:

`sudo systemctl enable --now nutshell.service`

Now restart your machine and test whether Bitcoin Core, Litd, Nutshell and all other service start up properly.

You can follow the logs with:

`journalctl -f -u nutshell.service`

[[Install Nutshell]]

First we are going to shut down LNbits, if it's still running. We can do that with `Ctr` + `C` in the window that it's running.

We are going to create a service file

```shell
sudo nano /etc/systemd/system/lnbits.service
```

Here's a service file we can use:

```
[Unit]
Description=LNbits
After=litd.service
Wants=litd.service

[Service]
User=ubuntu
WorkingDirectory=/home/ubuntu/git/lnbits
ExecStart=/home/ubuntu/.local/bin/poetry run lnbits --port 5000
User=ubuntu
Restart=always
TimeoutSec=120
RestartSec=30
Environment=PYTHONUNBUFFERED=1

[Install]
WantedBy=multi-user.target
```

We'll save it with `Ctrl` + `O` and close the editor with `Ctrl` + `X`.

To activate the file, we are going to run:

```shell
sudo systemctl enable --now lnbits.service
```
We should see the following output: `Created symlink /etc/systemd/system/multi-user.target.wants/lnbits.service → /etc/systemd/system/lnbits.service.`

We can check if its running now with `systemctl status lnbits.service` and refresh the wallet we have open in our browser.

Now try restarting the machine and see if everything comes online by itself, including Bitcoin Core, LND and LNbits!

[[Install LNbits]]

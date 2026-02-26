You can access the user interface at `https://<ip address>:8443`

For example, if you are working directly on the machine that runs litd, this might be [https://127.0.0.1:8443](https://127.0.0.1:8443), or it might be the IP of your VPS: [https://172.81.181.220:8443/](https://172.81.181.220:8443/). If you are connecting to a computer on your home network, make sure you are on the same network (e.g. the same Wi-Fi). Your connection might look like this: [https://192.168.1.21:8443/](https://192.168.1.21:8443/)

As we are not able to obtain a certificate for this IP address, we will get the warning that this is a self-signed TLS certificate, which in almost all browsers we can "accept and continue."

Once we continue, we can enter our UI password.

It should be the same password that we can find in our `.lit/lit.conf` file.

Congratulations, we are connected to litd!

[[Run LND]]

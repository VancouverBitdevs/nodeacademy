As we want litd to keep running in the background even when we close the Terminal window, we will append `nohup` to the command.

```shell
nohup litd > /dev/null 2> ~/.lnd/err.log &
```

Press `Enter` and observe the logs. It might be very helpful at this stage to open a second Terminal window, ssh into your server and simply keep the logs running in one window, while we interact with the program in another. The LND logs can be very noisy, so we may have to occasionally restart the logs if they appear stuck.

```shell
tail -f ~/.lnd/logs/bitcoin/mainnet/lnd.log
```


[[Configure Tor]]
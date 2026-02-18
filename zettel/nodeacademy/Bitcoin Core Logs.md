We can now follow the log files with this command. Adjust the path if your bitcoin directory is elsewhere:

```
tail -f /mnt/bitcoin/debug.log
```

We can exit this log by pressing `Ctrl` + `C`.

You may exit the terminal now at any time by typing `exit`. Bitcoin Core should keep running as long as the computer is not turned off. You should be able to check on your progress anytime by logging into your machine and following the logs as above.

Your logs will likely show mostly lines like the ones below as it is syncing. The **progress** variable shows your approximate progress in percent, while the **date** shows the day on which the block was mined that your node just synchronized. The **height** variable shows the block height. You will notice that syncing through the first five to seven years of Bitcoin is relatively quick, while the past five years will take relatively long.

```
2025-08-20T02:36:42Z UpdateTip: new best=00000000000000008776caa976d96ed7906146f2c0c62b06b1f42015db6033c7 height=277020 version=0x00000002 log2_work=75.151666 tx=29924089 date='2013-12-26T08:53:01Z' progress=0.024338 cache=670.1MiB(5447553txo)
2025-08-20T02:36:42Z UpdateTip: new best=0000000000000002354b56bf3c2c3055d967d75bc4771944b23f5c4748e3ac9e height=277021 version=0x00000002 log2_work=75.151840 tx=29924312 date='2013-12-26T09:00:23Z' progress=0.024338 cache=670.1MiB(5447215txo)
2025-08-20T02:36:42Z UpdateTip: new best=0000000000000002e3a28c8b0b7d3f6de2737cc07f8adf74e887926a901a0d94 height=277022 version=0x00000002 log2_work=75.152015 tx=29924546 date='2013-12-26T09:07:01Z' progress=0.024338 cache=670.1MiB(5447221txo)
```

[[Starting Bitcoin Core]]


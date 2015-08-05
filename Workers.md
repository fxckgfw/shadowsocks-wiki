Shadowsocks supports spawning child processes like nginx.

You can use `--workers` to specify how many workers to use.

This argument is only supported on Unix and ssserver.

Currently UDP relay does not work well on multiple workers.
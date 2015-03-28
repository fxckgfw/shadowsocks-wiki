Shadowsocks supports graceful shutdown like nginx.

You can send `SIGQUIT` to sslocal or ssserver process. The process closes listening sockets but still serves alive connections, allowing you to start a new process on the same port. When all connections on the old process are closed, it will then exit.

If you are using workers, send `SIGQUIT` to the master process.

On Windows, please use `SIGTERM` instead.

Notice: only [some versions](https://github.com/shadowsocks/shadowsocks/wiki/Feature-Comparison-across-Different-Versions) support this feature.
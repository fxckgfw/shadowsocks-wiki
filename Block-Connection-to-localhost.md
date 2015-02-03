From 2.6.7, localhost is blocked by default. If you don't want it, use `--forbidden-ip=""`.

From 2.6.3, you can prevent the server from connecting to some IP like 127.0.0.1.

    ssserver -c /etc/shadowsocks.json --forbidden-ip 127.0.0.1,::1

Notice only IPv4 and IPv6 addresses are allowed. Blocking will be processed **after DNS**.

This is because if a client tries to visit a hostname, like `localhost` or a domain name
a user has pointed to 127.0.0.1, it will be resolved into `127.0.0.1` or `::1`.
Thus it will still get blocked.
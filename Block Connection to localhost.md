From 2.6.3, you can forbid the server to connect to some IP, i.e. 127.0.0.1.

    ssserver -c /etc/shadowsocks.json --forbidden-ip 127.0.0.1,::1

Notice only IPv4 and IPv6 addresses are allowed. This is because if a client
tries to visit a hostname, like `localhost`, it will be resolved into
`127.0.0.1` or `::1`, it still gets blocked.
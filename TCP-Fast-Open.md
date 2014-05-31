If both of your server and client are deployed on Linux 3.7+, you can turn on
fast_open for lower latency.

Turn on fast open temporarily:

    echo 3 > /proc/sys/net/ipv4/tcp_fastopen

Then set fast_open to true in your config.json.

To turn on fast open permanently, see [Optimizing Shadowsocks](https://github.com/clowwindy/shadowsocks/wiki/Optimizing-Shadowsocks).
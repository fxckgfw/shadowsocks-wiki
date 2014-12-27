If both of your server and client are deployed on Linux 3.7+, you can turn on
fast_open for lower latency.

First set `fast_open` to `true` in your config.json.

Then turn on fast open on your OS temporarily:

    echo 3 > /proc/sys/net/ipv4/tcp_fastopen

To turn on fast open permanently, see [Optimizing Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks).

Notice: only [some versions](https://github.com/shadowsocks/shadowsocks/wiki/Feature-Comparison-across-Different-Versions) support this feature.
If both of your server and client are deployed on Linux 3.7+, you can turn on
fast_open for lower latency.

Turn on fast open:

    echo 3 > /proc/sys/net/ipv4/tcp_fastopen

Then set fast_open to true in your config.json.
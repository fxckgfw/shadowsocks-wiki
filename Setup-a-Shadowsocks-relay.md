If you want your client connected to a Japan VPS, but you want a US IP.

    Client <--> Japan VPS <--> US VPS

### Easy version:

1. Setup Shadowsocks server as usual on US VPS.
2. Install socat on Japan VPS.
3. Run `socat TCP-LISTEN:8388,fork TCP:US_VPS_IP:8388` on Japan VPS.
4. Set your server to JAPAN_VPS_IP:8388 on your client.

### Better version:

For those who need high performance, use haproxy instead of socat.

For Debian 7.0:

On Japan VPS. Append the following line to `/etc/apt/sources.list`

    deb http://ftp.us.debian.org/debian/ wheezy-backports main

Run

    apt-get udpate
    apt-get install haproxy

Edit `/etc/haproxy/haproxy.cfg`

```
global
        ulimit-n  51200

defaults
        log	global
        mode	tcp
        option	dontlognull
        contimeout 1000
        clitimeout 150000
        srvtimeout 150000

frontend ss-in
        bind *:8388
        default_backend ss-out

backend ss-out
        server server1 US_VPS_IP:8388 maxconn 20480
```

Then run `haproxy -f /etc/haproxy/haproxy.cfg`
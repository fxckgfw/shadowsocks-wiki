If you want your client connected to a Japan VPS, but you want a US IP.

    Client <--> Japan VPS <--> US VPS

### Easy version:

1. Setup Shadowsocks server as usual on US VPS.
2. On Japan VPS, enable forwarding. Replace `US_VPS_IP` and `JAPAN_VPS_IP` with actual IP:

        sudo su
        echo 1 > /proc/sys/net/ipv4/ip_forward
        iptables -t nat -A PREROUTING -p tcp --dport 8388 -j DNAT --to-destination US_VPS_IP:8388
        iptables -t nat -A POSTROUTING -p tcp -d US_VPS_IP --dport 8388 -j SNAT --to-source JAPAN_VPS_IP

3. Set your server to JAPAN_VPS_IP:8388 on your client.

### Better version:

For those who want more control and better performance, use haproxy instead.
You can also enable load balance by adding multiple servers.

For Debian 7.0:

On Japan VPS. Append the following line to `/etc/apt/sources.list`

    deb http://ftp.us.debian.org/debian/ wheezy-backports main

Run

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
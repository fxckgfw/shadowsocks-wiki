If you see a lot of `error: too many open files` in your log, you should optimize your system.
This tutorial applies to all shadowsocks servers (Python, libev, etc).

On Debian 7:

Create `/etc/sysctl.d/local.conf` with the following content:

```
# max open files
fs.file-max = 51200
# max read buffer
net.core.rmem_max = 67108864
# max write buffer
net.core.wmem_max = 67108864
# default read buffer
net.core.rmem_default = 65536
# default write buffer
net.core.wmem_default = 65536
# max processor input queue
net.core.netdev_max_backlog = 4096
# max backlog
net.core.somaxconn = 4096

# resist SYN flood attacks
net.ipv4.tcp_syncookies = 1
# reuse timewait sockets when safe
net.ipv4.tcp_tw_reuse = 1
# turn off fast timewait sockets recycling
net.ipv4.tcp_tw_recycle = 0
# short FIN timeout
net.ipv4.tcp_fin_timeout = 30
# short keepalive time
net.ipv4.tcp_keepalive_time = 1200
# outbound port range
net.ipv4.ip_local_port_range = 10000 65000
# max SYN backlog
net.ipv4.tcp_max_syn_backlog = 4096
# max timewait sockets held by system simultaneously
net.ipv4.tcp_max_tw_buckets = 5000
# turn on TCP Fast Open on both client and server side
net.ipv4.tcp_fastopen = 3
# TCP receive buffer
net.ipv4.tcp_rmem = 4096 87380 67108864
# TCP write buffer
net.ipv4.tcp_wmem = 4096 65536 67108864
# turn on path MTU discovery
net.ipv4.tcp_mtu_probing = 1

# for high-latency network
net.ipv4.tcp_congestion_control = hybla

# for low-latency network, use cubic instead
# net.ipv4.tcp_congestion_control = cubic
```

Then:

    sysctl --system

Older system:

    sysctl -p /etc/sysctl.d/local.conf

Warning: **DO NOT ENABLE `net.ipv4.tcp_tw_recycle`!!!** See [this article](http://vincent.bernat.im/en/blog/2014-tcp-time-wait-state-linux.html).

If you use [Supervisor](https://github.com/shadowsocks/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor), Make sure you have the following line in `/etc/default/supervisor`. Once you added that line, restart Supervisor (`service stop supervisor && service start supervisor`).

```
ulimit -n 51200
```

If you run shadowsocks in the background in other ways, make sure to add `ulimit -n 51200` in your init script.

After optimizing, a busy Shadowsocks server that handles thousands of connections, takes about 30MB memory and 10% CPU. Notice that at the same time, **Linux kernel usually uses >100MB RAM** to hold buffer and cache for those connections. By using the sysctl config above, you are trading off RAM for speed. If you want to use less RAM, 
reduce the size of rmem and wmem.

![if_eth0-day](https://cloud.githubusercontent.com/assets/1073082/3358558/2a18bc5a-fadf-11e3-96c3-473c42f1a3a3.png)

![fw_conntrack-day](https://cloud.githubusercontent.com/assets/1073082/3358559/2bf8662e-fadf-11e3-8039-3d59bf689fe2.png)

![cpu-day](https://cloud.githubusercontent.com/assets/1073082/3358579/53951d80-fadf-11e3-8e6b-0ceed96950e2.png)

![proc_mem-day](https://cloud.githubusercontent.com/assets/1073082/3358599/87c98c08-fadf-11e3-9fc9-949f4061d2ca.png)

Before & after:

![cc](https://cloud.githubusercontent.com/assets/1073082/3296349/10c34b04-f5d9-11e3-95fc-e38f5299c274.jpg)
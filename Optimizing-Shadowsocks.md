On Debian 7:

Create /etc/sysctl.d/local.conf with the following content:

```
fs.file-max = 51200

net.core.rmem_max = 67108864 
net.core.wmem_max = 67108864 
net.core.netdev_max_backlog = 250000
net.core.somaxconn = 3240000

net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_fin_timeout = 30
net.ipv4.tcp_keepalive_time = 1200
net.ipv4.ip_local_port_range = 10000 65000
net.ipv4.tcp_max_syn_backlog = 8192
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_fastopen = 3
net.ipv4.tcp_rmem = 4096 87380 67108864
net.ipv4.tcp_wmem = 4096 65536 67108864
net.ipv4.tcp_mtu_probing = 1
net.ipv4.tcp_congestion_control = hybla
```

Then:

    sysctl -p

Warning: **DO NOT ENABLE `net.ipv4.tcp_tw_recycle`!!!** See [this article](http://vincent.bernat.im/en/blog/2014-tcp-time-wait-state-linux.html).

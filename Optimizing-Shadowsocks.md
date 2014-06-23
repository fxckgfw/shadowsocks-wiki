If you see a lot of `error: too many open files` in your log, you should optimize your system.
This tutorial applies to all shadowsocks servers (Python, libev, etc).

On Debian 7:

Create `/etc/sysctl.d/local.conf` with the following content:

```
fs.file-max = 51200

net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.core.rmem_default=65536
net.core.wmem_default=65536
net.core.netdev_max_backlog = 4096
net.core.somaxconn = 4096

net.ipv4.tcp_syncookies = 1
net.ipv4.tcp_tw_reuse = 1
net.ipv4.tcp_tw_recycle = 0
net.ipv4.tcp_fin_timeout = 30
net.ipv4.tcp_keepalive_time = 1200
net.ipv4.ip_local_port_range = 10000 65000
net.ipv4.tcp_max_syn_backlog = 4096
net.ipv4.tcp_max_tw_buckets = 5000
net.ipv4.tcp_fastopen = 3
net.ipv4.tcp_rmem = 4096 87380 67108864
net.ipv4.tcp_wmem = 4096 65536 67108864
net.ipv4.tcp_mtu_probing = 1
net.ipv4.tcp_congestion_control = hybla
```

Then:

    sysctl --system

Warning: **DO NOT ENABLE `net.ipv4.tcp_tw_recycle`!!!** See [this article](http://vincent.bernat.im/en/blog/2014-tcp-time-wait-state-linux.html).

If you use [Supervisor](https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor), Make sure you have the following line in `/etc/default/supervisor`. Once you added that line, restart Supervisor (`service stop supervisor && service start supervisor`).

```
ulimit -n 51200
```

If you use other ways to run shadowsocks in the background, make sure to add `ulimit -n 51200` in your init script.

After optimizing, Shadowsocks should be able to handle thousands of connections with about 20MB memory and < 10% CPU.

![if_eth0-day](https://cloud.githubusercontent.com/assets/1073082/3358558/2a18bc5a-fadf-11e3-96c3-473c42f1a3a3.png)

![fw_conntrack-day](https://cloud.githubusercontent.com/assets/1073082/3358559/2bf8662e-fadf-11e3-8039-3d59bf689fe2.png)

![cpu-day](https://cloud.githubusercontent.com/assets/1073082/3358579/53951d80-fadf-11e3-8e6b-0ceed96950e2.png)

![proc_mem-day](https://cloud.githubusercontent.com/assets/1073082/3358599/87c98c08-fadf-11e3-9fc9-949f4061d2ca.png)

Before & after:

![cc](https://cloud.githubusercontent.com/assets/1073082/3296349/10c34b04-f5d9-11e3-95fc-e38f5299c274.jpg)
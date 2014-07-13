如果您看到很多`error: too many open files`在你的日志中，这时你就应该优化你的系统了。
本教程适用于所有Shadowsocks服务端 （Python版、libev版、还有其他...）

以下教程适用于Debian7系统：

新建`/etc/sysctl.d/local.conf`这个文件并添加下面的内容：

```
fs.file-max = 51200

net.core.rmem_max = 67108864
net.core.wmem_max = 67108864
net.core.rmem_default = 65536
net.core.wmem_default = 65536
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

然后运行：

`sysctl --system`

注意：**不要开启`net.ipv4.tcp_tw_recycle`！！！**[看这个文章](http://vincent.bernat.im/en/blog/2014-tcp-time-wait-state-linux.html)。

如果你在使用[Supervisor](https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor)的话，请确保您的`/etc/default/supervisor`文件中有下面这一行。您一旦添加了这一行，请重启Supervisor（`service stop supervisor && service start supervisor`）

```
ulimit -n 51200
```

如果您通过其他方式来启动Shadowsocks，确保`ulimit -n 51200`在您的启动脚本中。

优化后，一个繁忙的处理很多连接数的Shadowsocks服务器，会占用30MB的内存以及10%的CPU。要注意的是在这个时候，**Linux 内核使用了 >100MB 内存**来缓冲和缓存这些连接。用了上面提供的sysctl设置后，你的内存速度会得到提升。如果你想用更少内存的话，减少rmem 以及 wmem。

![if_eth0-day](https://cloud.githubusercontent.com/assets/1073082/3358558/2a18bc5a-fadf-11e3-96c3-473c42f1a3a3.png)

![fw_conntrack-day](https://cloud.githubusercontent.com/assets/1073082/3358559/2bf8662e-fadf-11e3-8039-3d59bf689fe2.png)

![cpu-day](https://cloud.githubusercontent.com/assets/1073082/3358579/53951d80-fadf-11e3-8e6b-0ceed96950e2.png)

![proc_mem-day](https://cloud.githubusercontent.com/assets/1073082/3358599/87c98c08-fadf-11e3-9fc9-949f4061d2ca.png)

Before & after:

![cc](https://cloud.githubusercontent.com/assets/1073082/3296349/10c34b04-f5d9-11e3-95fc-e38f5299c274.jpg)
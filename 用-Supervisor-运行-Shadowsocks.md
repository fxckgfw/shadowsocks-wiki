如果你想在后台运行 Shadowsocks，可以使用 Supervisor，它可以方便地监控和控制任何程序，实现开机自动启动和后台运行。

下面是 Debian 和 Ubuntu 上的配置方法（如果你是 Linux 新手，不需要 SELinux，也不了解防火墙配置，也弄不清楚 RHEL 和 CentOS 的版本机制，那就用 Debian 或 Ubuntu 吧，别折腾了）：

执行
```
apt-get update
apt-get install python-pip python-m2crypto supervisor
pip install shadowsocks
```

编辑 `/etc/shadowsocks.json`

```
{
    "server":"my ip",
    "server_port":8388,
    "local_port":1080,
    "password":"my password",
    "timeout":600,
    "method":"aes-256-cfb"
}
```

编辑 `/etc/supervisor/conf.d/shadowsocks.conf`

```
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autorestart=true
user=nobody
```
如果端口 < 1024，把上面的 user=nobody 改成 user=root。

在 `/etc/default/supervisor` 最后加一行：

```
ulimit -n 51200
```

执行
```
service supervisor start
supervisorctl reload
```
就好了。

你可以检查日志或者控制 Shadowsocks 的运行：
```
supervisorctl tail -f shadowsocks stderr
supervisorctl restart shadowsocks
```

如果更新了 Supervisor 的配置文件（`/etc/supervisor.d/*.conf`），可以 `supervisorctl update` 来更新配置。
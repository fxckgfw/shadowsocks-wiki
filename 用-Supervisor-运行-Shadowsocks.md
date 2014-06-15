如果你想在后台运行 Shadowsocks，可以使用 supervisor。

以 Debian 7.0 为例：

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
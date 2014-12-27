[中文版](https://github.com/shadowsocks/shadowsocks/wiki/%E7%94%A8-Supervisor-%E8%BF%90%E8%A1%8C-Shadowsocks)

**Notice: from Shadowsocks 2.6, you can run Shadowsocks directly in the background without Supervisor.
This saves RAM for the extra supervisor process.**

    ssserver -c /etc/shadowsocks.json -d start
    ssserver -c /etc/shadowsocks.json -d stop

For old versions:

Edit `/etc/shadowsocks.json`

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

Run
```
apt-get update
apt-get install python-pip python-m2crypto supervisor
pip install shadowsocks
```

Edit `/etc/supervisor/conf.d/shadowsocks.conf`

```
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autorestart=true
user=nobody
```

Add the following line into `/etc/default/supervisor`

```
ulimit -n 51200
```

Run
```
service supervisor start
supervisorctl reload
```
Now it's up.

You can check logs or control the shadowsocks process:
```
supervisorctl tail -f shadowsocks stderr
supervisorctl restart shadowsocks
```
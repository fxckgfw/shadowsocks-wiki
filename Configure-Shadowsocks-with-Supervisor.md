[中文版](https://github.com/clowwindy/shadowsocks/wiki/%E7%94%A8-Supervisor-%E8%BF%90%E8%A1%8C-Shadowsocks)

If you want to run Shadowsocks in the background, use supervisor.

Here is an example of running shadowsocks with supervisor on Debian 7.0:

Run
```
apt-get update
apt-get install python-pip python-m2crypto supervisor
pip install shadowsocks
```

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
Here is an example of running shadowsocks with [supervisor](http://supervisord.org/index.html):

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
apt-get install python-pip python-m2crypto python-gevent supervisor
pip install shadowsocks
pip install superlance
```

Edit `/etc/supervisor/conf.d/shadowsocks.conf`

```
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autorestart=true
user=nobody

[eventlistener:crashmail]
command=/usr/local/bin/crashmail -a -m my@email.com
events=PROCESS_STATE
```

Run
```
supervisorctl reload
```
Now it's up.

You can check shadowsocks status:
```
supervisorctl status
supervisorctl tail shadowsocks
```
[中文版](https://github.com/clowwindy/shadowsocks/wiki/%E7%94%A8-Supervisor-%E8%BF%90%E8%A1%8C-Shadowsocks)

If you want to run Shadowsocks in the background, use supervisor.

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

Debian
------

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

CentOS
------

Run

```
yum install python-setuptools supervisor
easy_install pip
pip install shadowsocks
```

Edit `/etc/supervisord.conf`, add

```
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autorestart=true
user=nobody
```

Run

```
sudo chkconfig --add supervisord
sudo chkconfig supervisord on
service supervisor start
supervisorctl reload
```

Edit `/etc/sysconfig/iptables`, add

    -A INPUT -m state --state NEW -m tcp -p tcp --dport your_server_port -j ACCEPT
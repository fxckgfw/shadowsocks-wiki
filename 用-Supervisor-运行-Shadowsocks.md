**说明： 从 Shadowsocks 2.6 开始，你可以直接在后台运行 Shadowsocks，无需 Supervisor 。
这样省掉了 Supervisor 进程占用的内存。**

    ssserver -c /etc/shadowsocks.json -d start
    ssserver -c /etc/shadowsocks.json -d stop

对于老版本：

编辑 `/etc/shadowsocks.json`


    {
        "server":"0.0.0.0",
        "server_port":7325,
        "local_port":1080,
        "password":"my password",
        "timeout":600,
        "method":"aes-256-cfb"
    }

记得改密码和服务端端口，不要用默认的。

执行

    apt-get update
    apt-get install python-pip python-m2crypto supervisor
    pip install shadowsocks


编辑 `/etc/supervisor/conf.d/shadowsocks.conf`


    [program:shadowsocks]
    command=ssserver -c /etc/shadowsocks.json
    autorestart=true
    user=nobody

如果端口 < 1024，把上面的 user=nobody 改成 user=root。

在 `/etc/default/supervisor` 最后加一行：

    ulimit -n 51200

执行

    service supervisor start
    supervisorctl reload

如果遇到问题，可以检查日志：

    supervisorctl tail -f shadowsocks stderr

如果修改了 shadowsocks 配置 `/etc/shadowsocks.json`，
可以重启 shadowsocks：

    supervisorctl restart shadowsocks

如果修改了 Supervisor 的配置文件 `/etc/supervisor/*`，
可以更新 supervisor 配置：

    supervisorctl update
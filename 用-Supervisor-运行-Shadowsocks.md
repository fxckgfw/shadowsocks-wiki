如果你想在后台运行 Shadowsocks，可以使用 supervisor。

Supervisor是一个C/S系统,它可以在类UNIX系统上控制系统进程，由python编写，它提供了大量的功能来实现对进程的管理。

###安装
- pip

        pip install supervisor

- easy_install

        easy_install supervisor

- apt-get (Debian/Ubuntu)

        apt-get update
        apt-get install supervisor
        #默认配置文件在`/etc/supervisor/supervisord.conf`

- yum (Centos)

        yum install supervisor

###创建配置文件

安装完成后，使用下面两种方式之一创建默认配置文件：
- 默认路径(`apt-get`方式在`/etc/supervisor/supervisord.conf`)

        echo_supervisord_conf > /etc/supervisord.conf
        #supervisord程序在运行后会自动查找并加载此目录配置文件。

- 指定路径

        echo_supervisord_conf > "指定路径"/supervisord.conf
        #supervisord程序使用-c参数在启动时手动指定配置文件：`supervisord -c "指定路径"/supervisord.conf`。

###添加shadowsocks
编辑配置文件supervisord.conf，在后面添加

	[program:shadowsocks]
	command=ssserver -c /etc/shadowsocks.json
	autostart=true
	autorestart=true
	user=nobody
###启动

- 默认路径配置启动：`supervisord`

- 指定路径配置启动：`supervisord -c "指定路径"/supervisord.conf`

###常用命令

- 获得所有程序状态 `supervisorctl status`
- 关闭目标程序 `supervisorctl stop ssserver`
- 启动目标程序 `supervisorctl start ssserver`
- 关闭所有程序 `supervisorctl shutdown`

---
###以 Debian 7.0 为例

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
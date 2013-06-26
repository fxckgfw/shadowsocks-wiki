shadowsocks
===========

shadowsocks 是一个轻量级隧道代理，用来穿过防火墙。

其它的移植的版本见[这里](https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients).

使用
----

首先，检查 Python 版本，要有 2.6 or 2.7.

    $ python --version
    Python 2.6.8
    
安装 Shadowsocks.

    pip install shadowsocks
    
建一个文件 `config.json`，内容如下：

    {
        "server":"my_server_ip",
        "server_port":8388,
        "local_port":1080,
        "password":"barfoo!",
        "timeout":600,
        "method":"table"
    }

各字段的含义：

    server          服务器 IP (IPv4/IPv6)，注意这也将是服务端监听的 IP 地址
    server_port     服务器端口
    local_port      本地端端口
    password        用来加密的密码
    timeout         超时时间（秒）
    method          加密方法，可选择 "bf-cfb", "aes-256-cfb", "des-cfb", "rc4", 等等。默认是一种不安全的加密，推荐用 "aes-256-cfb"

在服务器上 `cd` 到 `config.json` 所在目录。运行 `ssserver`。如果想在后台一直运行，
`nohup ssserver > log &`.

同样的，在你自己本地的机器上运行 `sslocal`.

然后把浏览器代理改为如下即可：

    协议： socks5
    地址： 127.0.0.1
    端口： 刚才填的 local_port

推荐配合 AutoProxy 或者 Proxy SwitchySharp 一起使用。

命令行参数
-----------

可以用命令行参数覆盖 `config.json` 里的设置：

    sslocal -s 服务器地址 -p 服务器端口 -l 本地端端口 -k 密码 -m 加密方法
    ssserver -p 服务器端口 -k 密码 -m 加密方法
    ssserver -c /etc/shadowsocks/config.json

加密
----

默认加密方法 table 速度很快，但很不安全。推荐使用 "aes-256-cfb" 或者 "bf-cfb"。请不要使用 "rc4"，它不安全。

可选的加密方式：

- aes-128-cfb
- aes-192-cfb
- aes-256-cfb
- bf-cfb
- camellia-128-cfb
- camellia-192-cfb
- camellia-256-cfb
- cast5-cfb
- des-cfb
- idea-cfb
- rc2-cfb
- rc4
- seed-cfb
- table

如果想使用 table 之外的加密方法，要先安装 [M2Crypto](http://chandlerproject.org/Projects/MeTooCrypto).

Ubuntu:

    sudo apt-get install python-m2crypto

其它系统：

    pip install M2Crypto

注意，在有些系统上其中一些加密方法可能不可用。

性能
------------

安装 gevent 可以提高 Shadowsocks 的性能：

    $ sudo apt-get install python-gevent

或者：

    $ sudo apt-get install libevent-dev python-pip
    $ sudo pip install gevent

协议
-------
MIT

Bugs and Issues
----------------
请访问 [issue tracker](https://github.com/clowwindy/shadowsocks/issues?state=open)

邮件列表: http://groups.google.com/group/shadowsocks

[常见问题](https://github.com/clowwindy/shadowsocks/wiki/Troubleshooting)

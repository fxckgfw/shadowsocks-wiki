[![当前状态][1]][0]

shadowsocks 是一个可穿透防火墙的轻量代理。

安装方法
-------

确保你装了 Python 2.6 或者 2.7。

    $ python --version
    Python 2.6.8

安装 Shadowsocks.

#### Debian / Ubuntu:

    apt-get install build-essential python-pip python-m2crypto python-dev
    pip install gevent shadowsocks

#### CentOS:

    yum install m2crypto python-setuptools
    easy_install pip
    pip install shadowsocks

#### OS X:

    git clone https://github.com/clowwindy/M2Crypto.git
    cd M2Crypto
    pip install .
    pip install shadowsocks

#### Windows:

选一个 [图形客户端][7]。

使用方法
-------

创建一个配置文件 `/etc/shadowsocks.json` (或者放在别的目录下)。
示例：

    {
        "server":"服务器 IP 地址",
        "server_port":8388,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"mypassword",
        "timeout":300,
        "method":"aes-256-cfb",
        "fast_open": false,
        "workers": 1
    }

各个字段的意思：

| 字段名         | 含义                                            |
| ------------- | ----------------------------------------------- |
| server        | 服务端监听的地址                                  |
| server_port   | 服务端的端口                                     |
| local_address | 本地端监听的地址                                  |
| local_port    | 本地端的端口                                     |
| password      | 用于加密的密码                                    |
| timeout       | 超时时间，单位秒                                  |
| method        | 加密方法，推荐 "aes-256-cfb"                      |
| fast_open     | 是否使用 [TCP_FASTOPEN][2], true / false         |
| workers       | worker 数量，Unix/Linux 可用，如果不理解含义请不要改 |

在服务器上运行 `ssserver -c /etc/shadowsocks.json`。如果要在后台运行，
[请使用 supervisor][8].

在本地运行 `sslocal -c /etc/shadowsocks.json`。

把浏览器的代理设为：

    协议: socks5
    地址: 127.0.0.1
    端口: 你填的 local_port

推荐配合 AutoProxy 或者 Proxy SwitchySharp 使用 Shadowsocks。

命令行参数
---------

你可以用命令行参数覆盖 `config.json` 中的设置：

    sslocal -s server_name -p server_port -l local_port -k password -m bf-cfb
    ssserver -p server_port -k password -m bf-cfb --workers 2
    ssserver -c /etc/shadowsocks/config.json

gevent
------

如果你遇到一些奇怪的问题，如果你装的是 gevent 0.9.x, 更新到最新版，或者卸掉 gevent。

    pip install gevent --upgrade

Wiki
----

https://github.com/clowwindy/shadowsocks/wiki

协议
----
MIT

问题反馈
--------
请访问 [issue tracker][5]

邮件列表： http://groups.google.com/group/shadowsocks

[常见问题][6]

[0]: https://travis-ci.org/clowwindy/shadowsocks
[1]: https://travis-ci.org/clowwindy/shadowsocks.png?branch=master
[2]: https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open
[3]: https://github.com/clowwindy/shadowsocks/wiki/Shadowsocks-%E4%BD%BF%E7%94%A8%E8%AF%B4%E6%98%8E
[4]: http://chandlerproject.org/Projects/MeTooCrypto
[5]: https://github.com/clowwindy/shadowsocks/issues?state=open
[6]: https://github.com/clowwindy/shadowsocks/wiki/Troubleshooting
[7]: https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients
[8]: https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor
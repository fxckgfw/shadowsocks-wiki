[![PyPI 版本]][PyPI] [![构建状态]][Travis CI] 

一个可穿透防火墙的轻量代理。

安装方法
-------

#### Debian / Ubuntu:

    apt-get install python-pip python-m2crypto
    pip install gevent shadowsocks

#### CentOS:

    yum install m2crypto python-setuptools
    easy_install pip
    pip install shadowsocks

#### OS X:

    brew install swig
    git clone https://github.com/clowwindy/M2Crypto.git
    cd M2Crypto
    pip install .
    pip install shadowsocks

#### Windows:

选一个 [图形客户端]。

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
| fast_open     | 是否使用 [TCP_FASTOPEN], true / false            |
| workers       | worker 数量，Unix/Linux 可用，如果不理解含义请不要改 |

在服务器上运行 `ssserver -c /etc/shadowsocks.json`。如果要在后台运行，
[请使用 supervisor].

在本地运行 `sslocal -c /etc/shadowsocks.json`。

把浏览器的代理设为：

    协议: socks5
    地址: 127.0.0.1
    端口: 你填的 local_port

推荐配合 [SwitchySharp] 使用 Shadowsocks。

命令行参数
---------

你可以用命令行参数覆盖 `config.json` 中的设置：

    sslocal -s server_name -p server_port -l local_port -k password -m bf-cfb
    ssserver -p server_port -k password -m bf-cfb --workers 2
    ssserver -c /etc/shadowsocks/config.json

Wiki
----

https://github.com/clowwindy/shadowsocks/wiki

协议
----
MIT

问题反馈
--------
请访问 [Issue Tracker]

邮件列表： http://groups.google.com/group/shadowsocks

[常见问题]


[构建状态]:        https://img.shields.io/travis/clowwindy/shadowsocks/master.svg?style=flat
[图形客户端]:      https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients
[Issue Tracker]:  https://github.com/clowwindy/shadowsocks/issues?state=open
[PyPI]:           https://pypi.python.org/pypi/shadowsocks
[PyPI 版本]:       https://img.shields.io/pypi/v/shadowsocks.svg?style=flat
[Supervisor]:     https://github.com/clowwindy/shadowsocks/wiki/Configure-Shadowsocks-with-Supervisor
[TCP_FASTOPEN]:   https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open
[Travis CI]:      https://travis-ci.org/clowwindy/shadowsocks
[常见问题]:        https://github.com/clowwindy/shadowsocks/wiki/Troubleshooting
[SwitchySharp]:    https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm
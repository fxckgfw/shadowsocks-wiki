[![PyPI 版本]][PyPI] [![构建状态]][Travis CI] [![Coverage Status]][Coverage]

一个可穿透防火墙的轻量代理。

安装
----

你需要在本地装一个客户端，在远程服务器上搭一个服务端。

### 客户端

* [Windows] / [OS X]
* [Android] / [iOS]
* [OpenWRT]

### 服务端

#### Debian / Ubuntu:

    apt-get install python-pip
    pip install shadowsocks

如果你添加了 [Debian sid] 的源，可直接 `apt-get install shadowsocks`.

#### CentOS:

    yum install python-setuptools
    easy_install pip
    pip install shadowsocks

#### Windows:

下载安装 [OpenSSL for Windows]。然后类似 Linux 通过 easy_install 或 pip 来安装。
如果你不清楚如何使用 easy_install，也可以直接[下载]，然后用 `python shadowsocks/server.py`
代替下文的 `ssserver`。

服务器配置
---------

服务端安装好以后，创建一个配置文件 `/etc/shadowsocks.json`。
示例：

    {
        "server":"服务器 IP 地址",
        "server_port":8388,
        "local_address": "127.0.0.1",
        "local_port":1080,
        "password":"mypassword",
        "timeout":300,
        "method":"aes-256-cfb",
        "fast_open": false
    }

各个字段的意思：

| 字段名         | 含义                                            |
| ------------- | ----------------------------------------------- |
| server        | 服务端监听的地址，服务端可填写 0.0.0.0             |
| server_port   | 服务端的端口                                     |
| local_address | 本地端监听的地址                                  |
| local_port    | 本地端的端口                                     |
| password      | 用于加密的密码                                    |
| timeout       | 超时时间，单位秒                                  |
| method        | 默认 "aes-256-cfb"，参见[加密方法]                |
| fast_open     | 是否使用 [TCP_FASTOPEN], true / false            |
| workers       | worker 数量，Unix/Linux 可用，如果不理解含义请不要改 |

在服务器上：

前台运行：

    ssserver -c /etc/shadowsocks.json

后台运行：

    ssserver -c /etc/shadowsocks.json -d start
    ssserver -c /etc/shadowsocks.json -d stop

在客户端上填写和服务器端一样的配置。关于客户端的使用请参见各个客户端的说明。

如果想直接用命令行运行客户端，可以运行 `sslocal -c /etc/shadowsocks.json`。

命令行参数
---------

用 `-h` 查看所有参数。你可以用命令行参数覆盖 `config.json` 中的设置：

    sslocal -s server_name -p server_port -l local_port -k password -m bf-cfb
    ssserver -p server_port -k password -m bf-cfb --workers 2
    ssserver -c /etc/shadowsocks/config.json -d start --pid-file=/tmp/shadowsocks.pid
    ssserver -c /etc/shadowsocks/config.json -d stop --pid-file=/tmp/shadowsocks.pid

文档
----

所有的文档都可以在 Wiki 里找到：
https://github.com/shadowsocks/shadowsocks/wiki

协议
----
MIT

问题反馈
--------
* [常见问题]
* [邮件列表]
* [Issue Tracker]


[Coverage Status]:   https://jenkins.shadowvpn.org/result/shadowsocks
[Coverage]:          https://jenkins.shadowvpn.org/job/Shadowsocks/ws/htmlcov/index.html
[Windows]:        https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients#windows
[OS X]:           https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-%E5%B8%AE%E5%8A%A9
[Android]:        https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients#android
[Debian sid]:     https://packages.debian.org/unstable/python/shadowsocks
[iOS]:            https://github.com/shadowsocks/shadowsocks-iOS/wiki/Help
[OpenWRT]:        https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients#openwrt
[构建状态]:        https://img.shields.io/travis/shadowsocks/shadowsocks/master.svg?style=flat
[图形界面版本]:    https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients
[Issue Tracker]:  https://github.com/shadowsocks/shadowsocks/issues?state=open
[OpenSSL for Windows]: http://slproweb.com/products/Win32OpenSSL.html
[PyPI]:           https://pypi.python.org/pypi/shadowsocks
[PyPI 版本]:       https://img.shields.io/pypi/v/shadowsocks.svg?style=flat
[TCP_FASTOPEN]:   https://github.com/shadowsocks/shadowsocks/wiki/TCP-Fast-Open
[Travis CI]:      https://travis-ci.org/shadowsocks/shadowsocks
[加密方法]:        https://github.com/shadowsocks/shadowsocks/wiki/Encryption
[常见问题]:        https://github.com/shadowsocks/shadowsocks/wiki/Troubleshooting
[邮件列表]:        http://groups.google.com/group/shadowsocks
[下载]:           https://pypi.python.org/pypi/shadowsocks
[![PyPI 版本]][PyPI] [![构建状态]][Travis CI] 

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

下载安装 OpenSSL for Windows。然后类似 Linux 通过 easy_install 或 pip 来安装。
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
        "fast_open": false,
        "workers": 1
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

在服务器上运行 `ssserver -c /etc/shadowsocks.json` 即可。如果要在后台运行，
请使用 [supervisor].

在本地，用上文的客户端进行相应配置并运行客户端，然后设置浏览器代理。
如果客户端也希望使用命令行版，可以运行 `sslocal -c /etc/shadowsocks.json`。

Chrome 推荐使用 [SwitchySharp] 切换代理设置。把浏览器代理设为下列参数即可：

    协议: socks5
    地址: 127.0.0.1
    端口: 你填的 local_port

如果无法安装 [SwitchySharp]，可以先用下列参数启动 Chrome，强制它使用代理：

    Chrome.exe --proxy-server="socks5://127.0.0.1:1080" --host-resolver-rules="MAP * 0.0.0.0 , EXCLUDE localhost"

如果连 Chrome 都无法下载，找人帮你下一个 [Chrome 离线安装包]。

命令行参数
---------

你可以用命令行参数覆盖 `config.json` 中的设置：

    sslocal -s server_addr -p server_port -l local_port -k password -m bf-cfb
    ssserver -p server_port -k password -m bf-cfb --workers 2
    ssserver -c /etc/shadowsocks/config.json

用 `-h` 查看所有参数。

Wiki
----

所有的文档都可以在 Wiki 里找到：
https://github.com/clowwindy/shadowsocks/wiki

协议
----
MIT

问题反馈
--------
* [常见问题]
* [邮件列表]
* [Issue Tracker]


[Windows]:        https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients#windows
[OS X]:           https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-%E5%B8%AE%E5%8A%A9
[Android]:        https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients#android
[Debian sid]:     https://packages.debian.org/unstable/python/shadowsocks
[iOS]:            https://github.com/shadowsocks/shadowsocks-iOS/wiki/Help
[OpenWRT]:        https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients#openwrt
[构建状态]:        https://img.shields.io/travis/clowwindy/shadowsocks/master.svg?style=flat
[图形界面版本]:    https://github.com/clowwindy/shadowsocks/wiki/Ports-and-Clients
[Issue Tracker]:  https://github.com/clowwindy/shadowsocks/issues?state=open
[PyPI]:           https://pypi.python.org/pypi/shadowsocks
[PyPI 版本]:       https://img.shields.io/pypi/v/shadowsocks.svg?style=flat
[Supervisor]:     https://github.com/clowwindy/shadowsocks/wiki/%E7%94%A8-Supervisor-%E8%BF%90%E8%A1%8C-Shadowsocks
[TCP_FASTOPEN]:   https://github.com/clowwindy/shadowsocks/wiki/TCP-Fast-Open
[Travis CI]:      https://travis-ci.org/clowwindy/shadowsocks
[加密方法]:        https://github.com/clowwindy/shadowsocks/wiki/Encryption
[常见问题]:        https://github.com/clowwindy/shadowsocks/wiki/Troubleshooting
[邮件列表]:        http://groups.google.com/group/shadowsocks
[SwitchySharp]:    https://chrome.google.com/webstore/detail/proxy-switchysharp/dpplabbmogkhghncfbfdeeokoefdjegm
[Chrome 离线安装包]: https://support.google.com/installer/answer/126299?hl=zh-Hans
[下载]:           https://pypi.python.org/pypi/shadowsocks
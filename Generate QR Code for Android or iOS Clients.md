Shadowsocks Android and iOS supports QR Code configuration.

Update: now you can also scan QR code on Windows and OS X.

Protocol
========

You can encode your server configuration to a QR Code.

1. Put your configuration together like this:

        method:password@hostname:port

2. Transform it into base64:

        bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQ=

3. Prepend with `ss://`

        ss://bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQ=

4. Generate a QR Code from the url above.

Generate via GUI clients
========================

You can also generate QR Codes from some GUI clients:
- [Shadowsocks for Windows](https://github.com/shadowsocks/shadowsocks-csharp)
- [Shadowsocks for OS X](https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-Help)
- [Shadowsocks-Qt5](https://github.com/librehat/shadowsocks-qt5)
- [Shadowsocks GUI](https://github.com/shadowsocks/shadowsocks-gui)

![image](https://cloud.githubusercontent.com/assets/1073082/4605261/a345d9d4-51d6-11e4-94e8-a13a987567e7.png)

Generate via Command line
=========================

    pip install qrcode
    echo -n "ss://"`echo -n aes-256-cfb:password@1.2.3.4:8388 | base64` | qr

If you can't scan the code, try changing your terminal font.

![image](https://cloud.githubusercontent.com/assets/1073082/4605437/6a41d15a-51e1-11e4-801a-424b5add2009.png)

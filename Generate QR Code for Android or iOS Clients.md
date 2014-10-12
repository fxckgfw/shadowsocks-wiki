ShadowSocks Android and iOS supports QR Code configuration.

Protocol
========

You can encode your server configuration to a QR Code.

1. Put your configuration together like this:

        method:password@hostname:port

2. Transform it into base64:

        bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQ=

3. Prepend with `ss://`

        ss://bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQK

4. Generate a QR Code from the url above.

Generate via Command line
=========================

    pip install qrcode
    echo "ss://"`echo -n aes-256-cfb:password@1.2.3.4:8388 | base64` | qr

If you can't scan the code, try changing your terminal font.

![image](https://cloud.githubusercontent.com/assets/1073082/4605437/6a41d15a-51e1-11e4-801a-424b5add2009.png)

Generate via GUI clients
========================

You can also generate QR Codes with
[Shadowsocks GUI](https://github.com/shadowsocks/shadowsocks-gui)
or [Shadowsocks for OS X](https://github.com/shadowsocks/shadowsocks-iOS/wiki/Shadowsocks-for-OSX-Help):

![image](https://cloud.githubusercontent.com/assets/1073082/4577064/1fb3b754-4fb9-11e4-9ab3-215e80d8ef1e.png)

![image](https://cloud.githubusercontent.com/assets/1073082/4576995/92b0cf5e-4fb8-11e4-84ce-6db752f6ba69.png)

![image](https://cloud.githubusercontent.com/assets/1073082/4605261/a345d9d4-51d6-11e4-94e8-a13a987567e7.png)
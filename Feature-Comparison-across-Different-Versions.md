Here's the page answering questions: does A support B?

## Servers

                  | [Python]  |   [libev]   |    [Go]   | [node.js]
----------------- | --------- | ----------- | ----------| ---------
Fast Open         |     Y     |      Y      |      N    |     N
Multiple Users    |     Y     |      Y      |      Y    |     Y
Management API    |     Y     |      Y      |      N    |     N
Workers           |     Y     |      N      |      N    |     N
Graceful Restart  |     Y     |      N      |      N    |     N
ss-redir          |     N     |      Y      |      N    |     N
ss-tunnel         |     N     |      Y      |      N    |     N
UDP Relay         |     Y     |      Y      |      N    |     Y

## Clients

                   | [Windows] | [ShadowsocksX] | [Qt5] | [Android] | [iOS App Store] | [iOS Cydia]
------------------ | ------- | ------------ | --- | ------- | ------------- | ---------
System Proxy       |    Y    |      Y       |  N  |    Y    |        N      |     Y
CHNRoutes          |    Y    |      Y       |  N  |    Y    |        Y      |     Y
PAC Configuration  |    Y    |      Y       |  N  |    N    |        N      |     N
Profile Switching  |    Y    |      Y       |  Y  |    Y    |        N      |     Y
QR Code Scan       |    Y    |      Y       |  Y  |    Y    |        Y      |     Y
QR Code Generation |    Y    |      Y       |  Y  |    N    |        N      |     Y

[Python]: https://github.com/shadowsocks/shadowsocks
[libev]: https://github.com/shadowsocks/shadowsocks-libev
[Go]: https://github.com/shadowsocks/shadowsocks-go
[node.js]: https://github.com/shadowsocks/shadowsocks-nodejs
[Windows]: https://github.com/shadowsocks/shadowsocks-csharp
[ShadowsocksX]: https://github.com/shadowsocks/shadowsocks-iOS
[qt5]: https://github.com/librehat/shadowsocks-qt5
[Android]: https://github.com/shadowsocks/shadowsocks-android
[iOS App Store]: https://github.com/shadowsocks/shadowsocks-iOS
[iOS Cydia]: https://github.com/linusyang/MobileShadowSocks
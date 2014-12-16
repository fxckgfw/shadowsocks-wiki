Here's the page answering questions: does A support B?

## Servers

                  |  Python   |    libev    |     Go    |  node.js
----------------- | --------- | ----------- | ----------| ---------
Fast Open         |     Y     |      Y      |      N    |     N
Multiple Users    |     Y     |      N      |      Y    |     Y
Workers           |     Y     |      N      |      N    |     N
Graceful Restart  |     Y     |      N      |      N    |     N
ss-redir          |     N     |      Y      |      N    |     N
ss-tunnel         |     N     |      Y      |      N    |     N
UDP Relay         |     Y     |      Y      |      N    |     Y

## Clients

                   | Windows | ShadowsocksX | Android | iOS App Store | iOS Cydia
------------------ | ------- | ------------ | ------- | ------------- | ---------
System Proxy       |    Y    |      Y       |    Y    |        N      |     Y
CHNRoutes          |    Y    |      Y       |    Y    |        Y      |     Y
PAC Configuration  |    Y    |      Y       |    N    |        N      |     N
Profile Switching  |    Y    |      Y       |    Y    |        N      |     Y
QR Code Scan       |    N    |      N       |    Y    |        Y      |     Y
QR Code Generation |    Y    |      Y       |    N    |        N      |     N

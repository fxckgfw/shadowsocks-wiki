Setup OpenVPN and Shadowsocks (Python / Node.js) on your server.

Setup OpenVPN client and Shadowsocks(Python / Node.js) on your local machine.

Connect Shadowsocks.

Add these lines to your .ovpn file:

    socks-proxy 127.0.0.1 1080
    route SHADOWSOCKS_SERVER_IP 255.255.255.255 net_gateway

Then connect OpenVPN.

Notice: only [versions that support UDP relay](https://github.com/shadowsocks/shadowsocks/wiki/Feature-Comparison-across-Different-Versions) support this feature.
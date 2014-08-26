Setup OpenVPN and shadowsocks (Python / node.js version) on your server.

Setup OpenVPN client and shadowsocks(Python / node.js) on your local machine.

Connect shadowsocks.

Add these lines to your .ovpn file:

    socks-proxy 127.0.0.1 1080
    route SHADOWSOCKS_SERVER_IP 255.255.255.255 net_gateway

Then connect OpenVPN.
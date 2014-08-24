Setup OpenVPN and shadowsocks (Python / libev / node.js version) on your server.

Setup OpenVPN client and shadowsocks(Python / GUI / libev version) on your local machine.

Connect shadowsocks.

Add these lines to your .ovpn file:

    socks-proxy 127.0.0.1 1080
    route SHADOWSOCKS_SERVER_IP 255.255.255.255 net_gateway

And make sure both server and client is configured to the TCP mode

    proto tcp

Then connect OpenVPN.
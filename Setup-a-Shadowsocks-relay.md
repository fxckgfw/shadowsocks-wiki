If you want your client connected to a Japan VPS, but you want a US IP.

    Client <--> Japan VPS <--> US VPS

### Easy version:

1. Setup Shadowsocks server as usual on US VPS.
2. Install socat on Japan VPS.
3. Run `socat TCP-LISTEN:8388,fork TCP:US_VPS_IP:8388` on Japan VPS.
4. Set your server to JAPAN_VPS_IP:8388 on your client.

### Better version:

Append the following line to `/etc/apt/sources.list`

    deb http://ftp.us.debian.org/debian/ wheezy-backports main


If you share your server with strangers, you need to be careful. The numbers used below are just examples.

1. [Optimize your server](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)

2. Limit bandwidth

        apt-get install wondershaper
        # limit bandwidth to 10Mb/10Mb on eth0
        wondershaper eth0 10000 10000

3. Limit connections

        iptables -A INPUT -p tcp --syn --dport ${SHADOWSOCKS_PORT} -m connlimit --connlimit-above 32 -j REJECT --reject-with tcp-reset

4. Prevent ssh password cracking

        apt-get install denyhosts

5. [Prevent Shadowsocks password cracking](https://github.com/shadowsocks/shadowsocks/wiki/Ban-Brute-Force-Crackers)

6. [Block connection to localhost](https://github.com/shadowsocks/shadowsocks/wiki/Block-Connection-to-localhost)

7. Run Shadowsocks server as nonroot user

        sudo useradd ssuser
        sudo ssserver [other options] --user ssuser

8. Block traffic to non-HTTP port

        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 80 -j ACCEPT
        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 443 -j ACCEPT
        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp -j REJECT --reject-with tcp-reset

9. Block BitTorrent trackers

        apt-get install nginx

   Edit nginx configuration:

        server {
            listen 0.0.0.0:3128;
            resolver 8.8.8.8;
            location / {
                set $upstream_host $host;
            if ($request_uri ~ "^/announce.*") {
                    return 403;
                }
                if ($request_uri ~ "^.*torrent.*") {
                    return 403;
                }
                proxy_set_header Host $upstream_host;
                proxy_pass http://$upstream_host;
                proxy_buffering off;
            }
        }

  Redirect 80 port to nginx:

        iptables -t nat -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 80 -j REDIRECT --to-port 3128


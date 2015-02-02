If you share your server with strangers, you need to be careful.

1. Limit bandwidth

        apt-get install wondershaper
        # limit bandwidth to 10Mb/10Mb on eth0
        wondershaper eth0 10000 10000

2. Prevent ssh password cracking

        apt-get install denyhosts

3. [Prevent Shadowsocks password cracking](https://github.com/shadowsocks/shadowsocks/wiki/Ban-Brute-Force-Crackers)

4. [Block connection to localhost](https://github.com/shadowsocks/shadowsocks/wiki/Block-Connection-to-localhost)

5. Run Shadowsocks server as nonroot user

        sudo useradd ssuser
        sudo ssserver [other options] --user ssuser

6. Block traffic to non-HTTP port

        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 80 -j ACCEPT
        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp --dport 443 -j ACCEPT
        iptables -t filter -m owner --uid-owner ssuser -A OUTPUT -p tcp -j REJECT --reject-with tcp-reset

7. Block BitTorrent trackers

        apt-get install nginx

   Edit nginx configuration:

        server {
            listen 127.0.0.1:3128;
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

        iptables -t nat -m owner --uid-owner http-ss -A OUTPUT -p tcp --dport 80 -j REDIRECT --to-port 3128


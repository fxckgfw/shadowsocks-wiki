出现问题时，可以按下列步骤确定和诊断问题：

1. 先确定是本地的问题，还是服务端的问题。可以通过更换服务端（比如用别人的或者公共服务器），更换本地端（比如分别用手机和电脑测试）。
2. 查看本地端的日志来诊断本地端有没有收到浏览器的请求。如果本地端没有收到请求，检查浏览器代理设置，检查本地防火墙。如果日志中只有 IP 没有域名，确保你配置浏览器远程解析域名，否则本地需要做防 DNS 污染。
3. 查看服务端的日志来诊断服务端有没有收到本地端发来的请求。如果服务端没有收到请求，检查服务器防火墙，在本地用 tcping 等端口扫描工具检查服务器端口有没有打开。尝试更换 IP 或端口。
4. 如果服务端收到了请求，但浏览器没有载入内容，检查服务端的 DNS `/etc/resolv.conf`，改为 `8.8.8.8` 再重启服务端。
5. 如果服务端速度慢，可能无良 ISP 做了 QoS，更换端口到 `80` `25` `443` `995` `3389` 等常用端口再测试。
6. 如果服务端启动时提示权限问题，可能是系统限制了 <1024 端口权限，用 iptables 做转发即可 `iptables -t nat -A PREROUTING -p tcp --dport 995 -j REDIRECT --to-ports 8387`
7. 如果访问特定的网站有问题，打开浏览器开发者工具网络部分，看一下哪个请求卡住了，然后在服务器上尝试用 ping curl 等工具检查这个请求的 URL 和主机的联通性。并检查这个请求的 URL 是不是被你的 PAC 规则排除了。

When you have problems, follow the steps below to diagnose:

1. Check whether the problem is caused by client or server. Replace your server with public server and check again; replace your client with others like mobile or another client version.
2. Check client logs to see if the client received requests from your browser. If the client did not receive any requests, check proxy settings and local firewall.
3. Check server logs to see if the server received requests from your client. If the server did not receive any requests, check server firewall and use `tcping` to check server port.
4. If the server received requests but your browser got no responses, check the DNS on your server. Change it into `8.8.8.8`, restart your server and test again.
5. If the server is slow, change your server port into common port like `80` `25` `443` `995` `3389`.
6. If you see `Permission Denied` when server starts, use `iptables` to redirect ports<1024 to ports>1024 `iptables -t nat -A PREROUTING -p tcp --dport 995 -j REDIRECT --to-ports 8387`
7. If you have connection problem only to a specific website, open developer console and check which request block the loading process. Check its url and hostname, and use `ping` `curl` to check connectivity from your server to that url and hostname. Also check if this URL is bypassed by your PAC.
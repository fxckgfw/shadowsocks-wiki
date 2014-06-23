出现问题时，请按下列步骤确定和诊断问题：

1. 先确定是本地的问题，还是服务端的问题。可以通过更换服务端（比如用别人的或者公共服务器），比如更换本地端（分别用手机和电脑测试）。
2. 查看本地端的日志来诊断本地端有没有收到请求。
3. 查看服务端的日志来诊断服务端有没有收到请求。
4. 如果本地端没有收到请求，检查浏览器代理设置，检查本地防火墙。如果日志中只有 IP 没有域名，确保你本地做了防 DNS 污染，否则就配置浏览器远程解析域名。
5. 如果服务端没有收到请求，检查服务器防火墙，在本地用 tcping 等端口扫描工具检查服务器端口有没有打开。
6. 如果服务端收到了请求，但浏览器没有载入内容，检查服务端的 DNS `/etc/resolv.conf`，改为 `8.8.8.8` 再重启服务端。

When you have problems, follow the steps below to diagnose:

1. Check whether the problem is caused by client or server. Replace your server with public server and check again; replace your client with others like mobile or another client version.
2. Check client logs to see if the client received requests from your browser.
3. Check server logs to see if the server received requests from your client.
4. If the client did not receive any requests, check proxy settings and local firewall.
5. If the server did not receive any requests, check server firewall and use `tcping` to check server port.
6. If the server received requests but your browser got no responses, check the DNS on your server. Change it into `8.8.8.8`, restart your server and test again.
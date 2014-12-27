也适用于除了 Linode 之外的所有 Xen 的 Debian 7 VPS。如果你已经建了一个 Debian 7.0+ 节点，在节点上执行下列命令并跳到步骤 6。
```
apt-get install curl
curl 'https://raw.githubusercontent.com/shadowsocks/stackscript/master/stackscript.sh?v=4' > /tmp/ss.sh && bash /tmp/ss.sh && rm /tmp/ss.sh
```

如果你没有创建节点：

1. 创建一个节点，在部署界面选择 `Deploying using StackScripts`
    * ![88be8e49-2018-476c-8380-424ee8470561](https://cloud.githubusercontent.com/assets/1073082/3285904/fa5fc7b8-f540-11e3-948e-95a30d2d320b.png)
2. 搜索 Shadowsocks，点它：
    * ![screen shot 2014-06-16 at 6 24 23 pm](https://cloud.githubusercontent.com/assets/1073082/3285908/0037b6be-f541-11e3-8881-000a8dc38f7c.png)
3. 设置 root 密码，点 rebuild
    * ![screen shot 2014-06-16 at 6 25 50 pm](https://cloud.githubusercontent.com/assets/1073082/3285916/0a27667e-f541-11e3-8408-4691c421e550.png)
4. 到节点界面点开机
    * ![0fdd081e-5288-4dcf-ae52-351e94ed1667](https://cloud.githubusercontent.com/assets/1073082/3285906/fda3820c-f540-11e3-8b1a-73f6cfbfd67f.png)
5. 等 VPS 启动
6. 登录服务器，检查是否一切正常。

```
# supervisorctl status
shadowsocks                      RUNNING    pid 6929, uptime 0:01:25
# supervisorctl tail shadowsocks stderr
2014-06-16 10:28:00 INFO     starting server at 0.0.0.0:4762
```

获取随机生成的密码和端口号：
```
# cat /etc/shadowsocks.json 
{
    "server":"0.0.0.0",
    "server_port":4762,
    "local_port":1080,
    "password":"8d779a1ee2db776db8e20adffaa12d0c",
    "timeout":300,
    "method":"aes-256-cfb"
}
```

如果需要重启服务，执行：

    supervisorctl restart shadowsocks

注：使用本安装脚本会自动[优化系统参数](https://github.com/shadowsocks/shadowsocks/wiki/Optimizing-Shadowsocks)。不过其中 hybla 算法的优化需要[更换内核](https://library.linode.com/custom-instances/pv-grub-howto#sph_debian-7-wheezy)后才能生效。
If you already created a [Linode] with Debian 7.0+, run the following and skip to Step 6.
```
apt-get install curl
curl 'https://raw.githubusercontent.com/shadowsocks/stackscript/master/stackscript.sh?v=4' > /tmp/ss.sh && bash /tmp/ss.sh && rm /tmp/ss.sh
```

If you didn't, do the following:

1. Create a new Linode and select `Deploying using StackScripts`
    * ![88be8e49-2018-476c-8380-424ee8470561](https://cloud.githubusercontent.com/assets/1073082/3285904/fa5fc7b8-f540-11e3-948e-95a30d2d320b.png)
2. Search Shadowsocks StackScript written by clowwindy and click it
    * ![screen shot 2014-06-16 at 6 24 23 pm](https://cloud.githubusercontent.com/assets/1073082/3285908/0037b6be-f541-11e3-8881-000a8dc38f7c.png)
3. Set root password and rebuild your server
    * ![screen shot 2014-06-16 at 6 25 50 pm](https://cloud.githubusercontent.com/assets/1073082/3285916/0a27667e-f541-11e3-8408-4691c421e550.png)
4. Boot your server
    * ![0fdd081e-5288-4dcf-ae52-351e94ed1667](https://cloud.githubusercontent.com/assets/1073082/3285906/fda3820c-f540-11e3-8b1a-73f6cfbfd67f.png)
5. Wait the VPS to boot up.
6. Log in to your server, check everything is OK. And find the password and server port generated for you:

```
# supervisorctl status
shadowsocks                      RUNNING    pid 6929, uptime 0:01:25
# cat /etc/shadowsocks.json 
{
    "server":"0.0.0.0",
    "server_port":4762,
    "local_port":1080,
    "password":"7f2aa2fef57d8414",
    "timeout":300,
    "method":"aes-256-cfb"
}
```

If you need to restart the server, run

    supervisorctl restart shadowsocks

[Linode]: https://www.linode.com/?r=e7932c8b03f9abc8aab71663b90b689a676402d1
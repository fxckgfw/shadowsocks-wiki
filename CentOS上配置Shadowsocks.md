## 首先做好必要的安全措施

配置fail2ban

```
sudo yum install fail2ban
sudo cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
sudo service fail2ban restart
```

## 安装shadowsocks、supervisor

前提是安装好[EPEL源][1]的情况下

`sudo yum install python-pip m2crypto supervisor`

`sudo pip install shadowsocks`

## 添加shadowsocks配置文件

`sudo nano /etc/shadowsocks.json`

示例

```
{
    "server":"0.0.0.0",
    "server_port":7325,
    "local_port":1080,
    "password":"my password",
    "timeout":600,
    "method":"aes-256-cfb"
}
```

## 配置supervisor [拓展阅读][2]

`sudo nano /etc/supervisord.conf`

添加

```
[program:shadowsocks]
command=ssserver -c /etc/shadowsocks.json
autorestart=true
user=nobody
```

## 让supervisor自启动

`sudo chkconfig --add supervisord`

`sudo chkconfig supervisord on`

## 配置防火墙

`sudo nano /etc/sysconfig/iptables`

加上

`-A INPUT -m state --state NEW -m tcp -p tcp --dport 你的端口 -j ACCEPT`

 [1]: http://www.ivancai.me/2014/10/24/centos-epel.html
 [2]: http://www.ivancai.me/2014/10/24/centos-install-supervisor.html
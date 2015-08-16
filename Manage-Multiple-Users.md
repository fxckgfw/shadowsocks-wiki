If you want to build a user management system, Shadowsocks provides an API that allows you to add/remove ports on the fly, as well as get transfer statistics from Shadowsocks.

If you simply want to add multiple users without changing them on the fly, you can check [this tutorial](https://github.com/shadowsocks/shadowsocks/wiki/Configure-Multiple-Users).

Notice: only Python and libev versions support this feature.

Setup
-----

Enable manager API by specifying `--manager-address`, which is either a Unix socket or an IP address:
```
# Use a Unix socket
ssserver --manager-address /var/run/shadowsocks-manager.sock -c tests/server-multi-passwd.json
# Use an IP address
ssserver --manager-address 127.0.0.1:6001 -c tests/server-multi-passwd.json
```

For security reasons, you should use Unix sockets.

When manager is enabled, [workers](https://github.com/shadowsocks/shadowsocks/wiki/Workers) and [graceful restart](https://github.com/shadowsocks/shadowsocks/wiki/Graceful-shutdown-and-restart) are disabled.

Protocol
--------

You can send UDP data to Shadowsocks.

```
command[: JSON data]
```

To add a port:

```
add: {"server_port": 8001, "password":"7cd308cc059"}
```

To remove a port:

```
remove: {"server_port": 8001}
```

To receive a pong:

```
ping
```

Shadowsocks will send back transfer statistics:

```
stat: {"8001":11370}
```

Example Code
------------

Here's code that demonstrates how to talk to the Shadowsocks server:
```
import socket

cli = socket.socket(socket.AF_UNIX, socket.SOCK_DGRAM)
cli.bind('/tmp/client.sock')  # address of the client
cli.connect('/var/run/shadowsocks-manager.sock')  # address of Shadowsocks manager

cli.send(b'ping')
print(cli.recv(1506))  # You'll receive 'pong'

cli.send(b'add: {"server_port":8001, "password":"7cd308cc059"}')
print(cli.recv(1506))  # You'll receive 'ok'

cli.send(b'remove: {"server_port":8001}')
print(cli.recv(1506))  # You'll receive 'ok'

while True:
    print(cli.recv(1506))  # when data is transferred on Shadowsocks, you'll receive stat info every 10 seconds
```
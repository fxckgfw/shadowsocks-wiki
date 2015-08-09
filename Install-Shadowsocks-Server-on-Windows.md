Notice: this page is for **server side**. If you are looking for clients, visit [clients](https://github.com/shadowsocks/shadowsocks/wiki/Ports-and-Clients#windows).

Server deployment on Windows is discouraged, since the `select` API performs very poor. If you want to serve many users, you should always set up your server on Linux. Please visit [README](https://github.com/shadowsocks/shadowsocks/blob/master/README.md) for more details.

1. Download and install [Python for Windows](https://www.python.org/downloads/windows/), you can download x86-64 MSI installer in 64bit Windows.
2. During installation you should install `pip`  
![Python](https://cloud.githubusercontent.com/assets/493124/5639371/0b91b9fa-9650-11e4-9782-44526d25f2fa.png)
3. Install [OpenSSL for Windows](https://slproweb.com/products/Win32OpenSSL.html). If you installed 64bit Python, you should install 64bit OpenSSL.
4. Install shadowsocks like Linux. In Command Prompt, type command line  
    ````
     pip install shadowsocks
    ````
5. If you want to use `salsa20` or `chacha20` encryption, download [libsodium](http://download.libsodium.org/libsodium/releases/) and put dll files (without path) into `C:\Windows\System32` or `C:\Windows\SysWOW64` (32bit Python on 64bit Windows).
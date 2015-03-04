First, set up shadowsocks as usual. Suppose your local is running on 127.0.0.1:1080.

Install [proxychains][1].

On Debian/Ubuntu:

    apt-get install proxychains

On Mac OS X:

    brew install proxychains-ng

Make a config file at `~/.proxychains/proxychains.conf` with content:

    strict_chain
    proxy_dns 
    remote_dns_subnet 224
    tcp_read_time_out 15000
    tcp_connect_time_out 8000
    localnet 127.0.0.0/255.0.0.0
    quiet_mode
    
    [ProxyList]
    socks5  127.0.0.1 1080


Then run command with proxychains. Examples:

    proxychains4 curl https://www.twitter.com/
    proxychains4 git push origin master

Or just proxify bash:

    proxychains4 bash
    curl https://www.twitter.com/
    git push origin master

[1]: http://proxychains.sourceforge.net/
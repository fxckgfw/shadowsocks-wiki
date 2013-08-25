* With the proxy set, I failed to load some websites, while the other websites seem normal  
    Check the logs of local.py. If you see only IP addresses instead of hostnames, your may have suffered DNS poisoning, but your browser hasn't 
    been configured to let the proxy resolve DNS.  
    To configure DNS properly, you can simply install **FoxyProxy or Autoproxy for Firefox, ProxySwitchy or SwitchySharp for 
    Chrome**. They will configure your browser automatically.  
    Or you can change network.proxy.socks_remote_dns into true in about:config page if you use Firefox.
* I can't load any websites, and the log prints `mode != 1`  
    Make sure proxy protocol is set to Socks5, not Socks4 or HTTP.
* I use IE and I can't get my proxy to work    
    Since you can't specify Socks4 or Socks5 in IE settings, you may want to use a PAC (Proxy auto-config) script, or 
    just use Chrome instead.
* (Nodejs version) When I use AES-256-CFB, I got some logs like `unsupported addrtype: 115`.  
    Upgrade your nodejs to the latest version.

If you have other problems, feel free to post questions to our [mailing list](http://groups.google.com/group/shadowsocks).
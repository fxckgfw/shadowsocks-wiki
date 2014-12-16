Currently Python and Go servers support multiple users.

You can use different passwords on different ports like this:

    {
        "server": "0.0.0.0",
        "port_password": {
            "8381": "foobar1",
            "8382": "foobar2",
            "8383": "foobar3",
            "8384": "foobar4"
        },
        "timeout": 300,
        "method": "aes-256-cfb"
    }

Notice: only [some versions](https://github.com/clowwindy/shadowsocks/wiki/Feature-Comparison-across-Different-Versions) support this feature.
Shadowsocks 2.6.2+ output the IPs that try to brute force crack your password.

You can use [utils/autoban.py](https://github.com/shadowsocks/shadowsocks/tree/master/utils) to ban them.

    python autoban.py < /var/log/shadowsocks.log

Use `-c` to specify with how many failure times it should be considered as an
attack. Default is 3.

To continue watching for the log file:

    nohup tail -F /var/log/shadowsocks.log | python autoban.py >log 2>log &

Use with caution. Avoid to ban yourself.
Supported Ciphers
=================

- aes-256-cfb: Default
- aes-128-cfb
- aes-192-cfb
- aes-256-ofb
- aes-128-ofb
- aes-192-ofb
- aes-128-ctr
- aes-192-ctr
- aes-256-ctr
- aes-128-cfb8
- aes-192-cfb8
- aes-256-cfb8
- aes-128-cfb1
- aes-192-cfb1
- aes-256-cfb1
- bf-cfb
- camellia-128-cfb
- camellia-192-cfb
- camellia-256-cfb
- cast5-cfb
- chacha20
- idea-cfb
- rc2-cfb
- rc4-md5
- salsa20
- seed-cfb

Installing `M2Crypto` will make encryption a little faster.

Debian:

    apt-get install python-m2crypto

CentOS:

    yum install m2crypto

rc4-md5
=======
`rc4-md5` is a safe, fast encryption that use different key per connection. It is recommended for OpenWRT routers.

salsa20 and chacha20
====================
`salsa20` and `chacha20` are fast stream ciphers. Optimized `salsa20` implementation on x86_64 is even 2x faster than `rc4` (but slightly slower on ARM).

Install [libsodium](https://github.com/jedisct1/libsodium) >= 1.0.0 if you want to use them.

You can use [this script](https://github.com/clowwindy/shadowsocks/blob/master/tests/libsodium/install.sh) to install it.

Deprecated Ciphers
==================
These legacy ciphers are either slow or not safe. Do not use them:
- rc4
- des-cfb
- table
- salsa20-ctr

Notice: not all Shadowsocks versions support every ciphers.
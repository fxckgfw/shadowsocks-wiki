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
- des-cfb
- idea-cfb
- rc2-cfb
- rc4-md5
- seed-cfb
- salsa20-ctr

rc4-md5
=======
`rc4-md5` is a safe, fast encryption that use different key per connection. It is recommended for OpenWRT routers.

salsa20-ctr
===========
salsa20-ctr is a fast stream cipher.

Install these packages if you want to use it:

Debian / Ubuntu:

    apt-get install python-numpy
    pip install salsa20

Deprecated Ciphers
==================
These ciphers are legacy and not safe. Do not use them:
- rc4
- table

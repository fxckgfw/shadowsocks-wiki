Currently we support these encryption methods:
- aes-256-cfb: Default and recommended.
- aes-128-cfb
- aes-192-cfb
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

`rc4-md5` is a safe, fast encryption that use different key per connection. It is recommended for OpenWRT routers.

These methods are legacy and not safe. Do not use them:
- rc4
- table

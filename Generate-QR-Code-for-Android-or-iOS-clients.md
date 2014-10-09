ShadowSocks Android and iOS supports QR Code configuration.

You can encode your server configuration to a QR Code.

1. Put your configuration together:

    method:password@hostname:port

2. Transform it into base64:

    bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQK

3. Prepend with `ss://`

    ss://bWV0aG9kOnBhc3N3b3JkQGhvc3RuYW1lOnBvcnQK

4. Generate a QR Code from the url above.

You can also generate QR Codes with Shadowsocks GUI:

![image](https://cloud.githubusercontent.com/assets/1073082/4577064/1fb3b754-4fb9-11e4-9ab3-215e80d8ef1e.png)

![image](https://cloud.githubusercontent.com/assets/1073082/4576995/92b0cf5e-4fb8-11e4-84ce-6db752f6ba69.png)


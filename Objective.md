SSL and VPN provides data security. To users in China and many other countries,
their goal is not to protect the data security, but to unblock YouTube and Facebook.

SSL and VPN failed because some of their protocol information is in plain text.
For example, firewalls can read certification information from SSL connections, and
block connections based on certification identity. In some countries, they just ban
all OpenVPN traffic.

Unlike SSL and VPN, Shadowsocks is designed for protocol anonymity, which means
its main objective is to make firewalls deployed on routers hard to tell Shadowsocks
from normal traffic.

If you need data securify, you can [wrap SSL or VPN inside Shadowsocks](https://github.com/shadowsocks/shadowsocks/wiki/Connect-to-OpenVPN-over-Shadowsocks).
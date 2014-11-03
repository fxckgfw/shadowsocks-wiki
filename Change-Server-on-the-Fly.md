Some clients(Shadowsocks-GUI, ShadowsocksX, GoAgentX) support choosing between different server profiles.

Notice due to Chrome's persistent connection to the proxy, you may need to force Chrome to reconnect to the proxy to connect to another Shadowsocks server. You can either restart your Shadowsocks client, or:

1. Open [chrome://net-internals/#sockets](chrome://net-internals/#sockets)
2. Click `Flush socket pools`.
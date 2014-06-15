Launch chrome with the following arguments:

    /path/to/Chrome.exe --proxy-server="socks5://127.0.0.1:1080" --host-resolver-rules="MAP * 0.0.0.0 , EXCLUDE localhost"

Reference:

http://www.chromium.org/developers/design-documents/network-stack/socks-proxy
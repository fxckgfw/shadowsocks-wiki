First run polipo with parent proxy set to Shadowsocks:

```bash
apt-get install polipo
service polipo stop
polipo socksParentProxy=localhost:1080
```

Then you can play with the HTTP proxy:

```bash
http_proxy=http://localhost:8123 apt-get update
```
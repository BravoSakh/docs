SOCKS5 Proxy
=====================

> apt-get update && apt-get upgrade

> apt-get install build-essential libwrap0-dev libpam0g-dev libkrb5-dev libsasl2-dev dante-server

> useradd --shell /usr/sbin/nologin socks5duser && passwd socks5duser

Сonfiguration Dante (/etc/danted.conf)
-----------------------------------

```
logoutput: stderr

internal: eth0 port = 9999
external: eth0
socksmethod: username
user.privileged: root
user.unprivileged: nobody

client pass {
       from: 0.0.0.0/0 port 1-65535 to: 0.0.0.0/0
       log: error
       socksmethod: username
}



socks pass {
       from: 0.0.0.0/0 to: 0.0.0.0/0
       command: bind connect udpassociate
       log: error
       socksmethod: username
}

socks pass {
       from: 0.0.0.0/0 to: 0.0.0.0/0
       command: bindreply udpreply
       log: error
}
```

> service danted restart


### Ex.: Telegram

> tg://socks?server=IP&port=PORT&user=USER&pass=PASS

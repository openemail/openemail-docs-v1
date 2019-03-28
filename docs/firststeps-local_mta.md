The easiest option would be to disable the listener on port 25/tcp.

**Postfix** users disable the listener by commenting the following line (starting with `smtp` or `25`) in `/etc/postfix/master.cf`:
```
#smtp      inet  n       -       -       -       -       smtpd
```

Furthermore, to relay over a dockerized openemail, you may want to add `172.22.1.1` as relayhost and remove the Docker interface from "inet_interfaces":

```
postconf -e 'relayhost = 172.22.1.1'
postconf -e "mynetworks = 127.0.0.0/8 [::ffff:127.0.0.0]/104 [::1]/128"
postconf -e "inet_interfaces = loopback-only"
postconf -e "relay_transport = relay"
postconf -e "default_transport = smtp"
```

**Now it is important** to not have the same FQDN in `myhostname` as you use for your dockerized openemail. Check your local (non-Docker) Postfix' main.cf for `myhostname` and set it to something different, for example `local.my.fqdn.tld`.

"172.22.1.1" is the openemail created network gateway in Docker.
Relaying over this interface is necessary (instead of - for example - relaying directly over ${OPENEMAIL_HOSTNAME}) to relay over a known internal network.

Restart Postfix after applying your changes.

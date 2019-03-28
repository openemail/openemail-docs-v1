## Attaching a Container to your Shell

To attach a container to your shell you can simply run

```
docker-compose exec $Service_Name /bin/bash
```

### Connecting to Services

If you want to connect to a service / application directly it is always a good idea to `source openemail.conf` to get all relevant variables into your environment.

#### MySQL

```
source openemail.conf
docker-compose exec mysql-openemail mysql -u${DBUSER} -p${DBPASS} ${DBNAME}
```

#### Redis

```
docker-compose exec redis-openemail redis-cli
```

## Service Descriptions

Here is a brief overview of what container / service does what:

| Service Name        | Service Descriptions                                                      |
| -----------------   | ------------------------------------------------------------------------- |
| unbound-openemail   | Local (DNSSEC) DNS Resolver                                               |
| mysql-openemail     | Stores SOGo's and most of openemail's settings                            |
| postfix-openemail   | Receives and sends mails                                                  |
| dovecot-openemail   | User logins and sieve filter                                              |
| redis-openemail     | Storage back-end for DKIM keys and Rspamd                                 |
| rspamd-openemail    | Mail filtering system. Used for av handling, dkim signing, spam handling  |
| clamd-openemail     | Scans attachments for viruses                                             |
| sogo-openemail      | Webmail client that handles Microsoft ActiveSync and Cal- / CardDav       |
| nginx-openemail     | Nginx remote proxy that handles all mailcow related HTTP / HTTPS requests |
| acme-openemail      | Automates HTTPS (SSL/TLS) certificate deployment                          |
| memcached-openemail | Internal caching system for openemail services                            |
| watchdog-openemail  | Allows the monitoring of docker containers / services                     |
| php-fpm-openemail   | Powers the openemail web UI                                               |
| netfilter-openemail | Fail2Ban like integration                                                 |

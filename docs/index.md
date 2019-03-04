
## What is openemail - Open Source Mail Server in Dockers 

At [Cybergate](https://cybergate.lk)  our effort to consolidate the best available open source email, collaboration, email security solutions together with other infrastructure components like backend databases, authentication services etc. to provide agile, secure, and enterprise ready world class email and collaboration platform that can easily replace any other equivalent commercial alternative.

Our administration backend web UI is a fork of [Mailcow](https://mailcow.email/) project. We are deeeply indebted to their excellent effort in making such a good consolidation of all complex backend tools into a single pane of web UI by making it very easy for administrators to manage the system without using complex command line tools and editing. 

Inspired by the concept of [Mailcow](https://mailcow.email/) each an every backend application in openemai is running in a docker container by making openemail as a software that is ready deploy in your private or public cloud infrastructure by utilizing the benefit of agile and elastic cloud infrastructure of the modern day computing. 

openemail has been designed to work as a highly scalable and agile software which you can use it to host from few mailboxes to millions of mailboxes which are required by services providers.  

As like any other  open source software  you are  free to use openemail at your own risk while you can obtained it as a supported and enterprise ready solution which is backed by [Cybergate](https://cybergate.lk) with its world class open source support team. 

Our enterprise support  subscriptions are supporting unlimited mail domains and accounts while our subscription is an annual SLA which is confined to several support levels of support types and hardware profiles, either physical or virtual, of the systems that you will be using to deploy openemail. You can have both on premise and hosted solution under these subscription contracts.

## Get support

### Commercial support

For commercial support contact [sales@cybergate.lk](mailto:sales@cybergate.lk) or get a support subscription at [Cybergate](https://www.cybergate.lk/openemail#support).

A fully featured managed mailcow is also available [here](https://www.servercow.de/mailcow#managed).

### Community support

- IRC @ [Freenode, #openemail](irc://irc.freenode.org:6667/openemail)
- GitHub @ [openemail](https://github.com/openemail/openemail)

## Demo

You can find a demo at [hasuna.openemail.io](https://hasuna.openemail.io), use the following credentials to login:

- **Administrator**: admin / openemail
- **Domain administrator**: domainadm / openemail
- **Mailbox**: demo@openemaill.io / openemail

## Overview

The integrated **openemail UI** allows administrative work on your mail server instance as well as separated domain administrator and mailbox user access:

- DKIM and ARC support
- Black- and whitelists per domain and per user
- Spam score management per-user (reject spam, mark spam, greylist)
- Allow mailbox users to create temporary spam aliases
- Prepend mail tags to subject or move mail to sub folder (per-user)
- Allow mailbox users to toggle incoming and outgoing TLS enforcement
- Allow users to reset SOGo ActiveSync device caches
- imapsync to migrate or pull remote mailboxes regularly
- TFA: Yubi OTP and U2F USB (Google Chrome and derivatives only), TOTP
- Add domains, mailboxes, aliases, domain aliases and SOGo resources
- Add whitelisted hosts to forward mail to mailcow
- Fail2ban-like integration
- Quarantine system
- A lot more...

mailcow: dockerized comes with multiple containers linked in one bridged network.
Each container represents a single application.

- Dovecot
- ClamAV (optional)
- Solr (optional)
- Memcached
- Redis
- MySQL
- Unbound (as resolver)
- PHP-FPM
- Postfix
- ACME-Client (thanks to @bebehei)
- Nginx
- Rspamd
- SOGo
- Netfilter (Fail2ban-like integration by @mkuron)
- Watchdog (basic monitoring)

**Docker volumes** to keep dynamic data - take care of them!

- vmail-vol-1
- solr-vol-1
- redis-vol-1
- mysql-vol-1
- rspamd-vol-1
- postfix-vol-1
- crypt-vol-1

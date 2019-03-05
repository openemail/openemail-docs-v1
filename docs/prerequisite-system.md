Before you run **openemail**, there are a few requirements that you should check:

!!! warning
    When running openemail on a Debian 8 (Jessie) box, you should [switch to kernel 4.9 from Jessie backports](https://packages.debian.org/jessie-backports/linux-image-amd64) to avoid a bug when running Docker containers with *healthchecks*! For more details read: [github.com/docker/docker/issues/30402](https://github.com/docker/docker/issues/30402)

!!! info
    - openemail requires [some ports](#default-ports) to be open for incoming connections, so make sure that your firewall is not blocking these port
    - Make sure that no other application is interfering with openemail's configuration, such as another mail service
    - A correct DNS setup is crucial to every good mailserver setup, so please make sure you got at least the [basics](prerequisite-dns/#the-minimal-dns-configuration) covered before you begin!
    - Make sure that your system has a correct date and [time setup](#date-and-time). This is crucial for stuff like two factor TOTP authentication.

## Minimum System Resources

Please make sure that your system has at least the following resources:

| Resource                | openemail                           |
| ----------------------- | ----------------------------------- |
| CPU                     | 1 GHz                               |
| RAM                     | 2 GiB + Swap (better: 4 GiB + Swap) |
| Disk                    | 5 GiB (without emails)              |
| System Type             | x86_64                              |

ClamAV and Solr are greedy RAM munchers. You can disable them in `openemail.conf` by settings SKIP_CLAMD=y and SKIP_SOLR=y.

## Firewall & Ports

Please check if any of openemail's standard ports are open and not in use by other applications:

```
# netstat -tulpn | grep -E -w '25|80|110|143|443|465|587|993|995'
```

!!! warning
    There are several problems with running openemail on a firewalld/ufw enabled system. You should disable it (if possible) and move your ruleset to the DOCKER-USER chain, which is not cleared by a Docker service restart, instead. See [this blog post](https://blog.donnex.net/docker-and-iptables-filtering/) for information about how to use iptables-persistent with the DOCKER-USER chain.
    As openemail runs dockerized, INPUT rules have no effect on restricting access to openemail. Use the FORWARD chain instead.

**

If this command returns any results please remove or stop the application running on that port. You may also adjust mailcows ports via the `mailcow.conf` configuration file.

### Default Ports

If you have a firewall in front of mailcow, please make sure that these ports are open for incoming connections:

| Service             | Protocol | Port   | Container         | Variable                         |
| --------------------|:--------:|:-------|:------------------|----------------------------------|
| Postfix SMTP        | TCP      | 25     | postfix-openemail | `${SMTP_PORT}`                   |
| Postfix SMTPS       | TCP      | 465    | postfix-openemail | `${SMTPS_PORT}`                  |
| Postfix Submission  | TCP      | 587    | postfix-openemail | `${SUBMISSION_PORT}`             |
| Dovecot IMAP        | TCP      | 143    | dovecot-openemail | `${IMAP_PORT}`                   |
| Dovecot IMAPS       | TCP      | 993    | dovecot-openemail | `${IMAPS_PORT}`                  |
| Dovecot POP3        | TCP      | 110    | dovecot-openemail | `${POP_PORT}`                    |
| Dovecot POP3S       | TCP      | 995    | dovecot-openemail | `${POPS_PORT}`                   |
| Dovecot ManageSieve | TCP      | 4190   | dovecot-openemail | `${SIEVE_PORT}`                  |
| HTTP(S)             | TCP      | 80/443 | nginx-openemail   | `${HTTP_PORT}` / `${HTTPS_PORT}` |

To bind a service to an IP address, you can prepend the IP like this: `SMTP_PORT=1.2.3.4:25`

**Important**: You cannot use IP:PORT bindings in HTTP_PORT and HTTPS_PORT. Please use `HTTP_PORT=1234` and `HTTP_BIND=1.2.3.4` instead.

## Date and Time

To ensure that you have the correct date and time setup on your system, please check the output of `timedatectl status`:

```
$ timedatectl status
                        Local time: Tue 2019-03-05 06:00:04 UTC
                  Universal time: Tue 2019-03-05 06:00:04 UTC
                        RTC time: Tue 2019-03-05 06:00:05
                       Time zone: Etc/UTC (UTC, +0000)
       System clock synchronized: yes
systemd-timesyncd.service active: yes
                 RTC in local TZ: no
```
The lines `NTP enabled: yes` and `NTP synchronized: yes` indicate wether you have NTP enabled and if it's synchronized.

To enable NTP you need to run the command `timedatectl set-ntp true`. You also need to edit your `/etc/systemd/timesyncd.conf`:

```
# vim /etc/systemd/timesyncd.conf
[Time]
Servers=0.pool.ntp.org 1.pool.ntp.org 2.pool.ntp.org 3.pool.ntp.org
```
```
$ chronyc tracking 
Reference ID    : 8B633576 (ip118.ip-139-99-53.net)
Stratum         : 3
Ref time (UTC)  : Tue Mar 05 06:22:37 2019
System time     : 0.000017628 seconds slow of NTP time
Last offset     : -0.000009700 seconds
RMS offset      : 0.000059413 seconds
Frequency       : 0.034 ppm fast
Residual freq   : -0.002 ppm
Skew            : 0.146 ppm
Root delay      : 0.001954436 seconds
Root dispersion : 0.001475935 seconds
Update interval : 130.1 seconds
Leap status     : Normal
```

## Hetzner Cloud (and probably others)

Check `/etc/network/interfaces.d/50-cloud-init.cfg` and change the IPv6 interface from eth0:0 to eth0:

```
# Wrong:
auto eth0:0
iface eth0:0 inet6 static
# Right:
auto eth0
iface eth0 inet6 static
```

Reboot or restart the interface.
You may want to [disable cloud-init network changes.](https://wiki.hetzner.de/index.php/Cloud_IP_static/en#disable_cloud-init_network_changes)

## MTU

Especially relevant for OpenStack users: Check your MTU and set it accordingly in docker-compose.yml. See **4.1** in [our installation docs](https://mailcow.github.io/mailcow-dockerized-docs/install/).

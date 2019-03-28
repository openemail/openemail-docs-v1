## **SNAT**

SNAT is used to change the source address of the packets sent by **openemail**.
It can be used to change the outgoing IP on systems with multiple IP addresses.

Open `openemail.conf`, set either or both of the following parameters:

```
# Use this IPv4 for outgoing connections (SNAT)
SNAT_TO_SOURCE=1.2.3.4

# Use this IPv6 for outgoing connections (SNAT)
SNAT6_TO_SOURCE=dead:beef
```

**To update the new settings run:**

```
docker-compose up -d
```
The values are read by netfilter-openemail. The container `netfilter-openemail` will make sure, the post-routing rules are on position 1 in the netfilter table. It does automatically delete and re-create them if they are found on another position than 1.

Check the output of `docker-compose logs --tail=200 netfilter-openemail to ensure the SNAT settings have been applied.

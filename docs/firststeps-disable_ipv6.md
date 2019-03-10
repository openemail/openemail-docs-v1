## **Disable IPV6**

This is **NOT** recommended!. But in case if you want to do it, it can be done.

If IPv6 MUST be disabled to fit a network, open `docker-compose.yml`, search for `enable_ipv6`...

```
networks:
  openemail-network:
    [...]
    enable_ipv6: true
    [...]
```

 and change it to `enable_ipv6: false`.

Then you need to shutdown Openemail, the containers removed and the network recreated executing the following commands.

```
docker-compose down
docker-compose up -d
```

## openemail Admin Account

Reset mailcow admin to `admin:moohoo`. Older mailcow: dockerized installations may find `openemail-reset-admin.sh` in their opoenemail root directory (openemail_path).

```
cd openemail_path
./helper-scripts/openemail-reset-admin.sh
```

## Reset MySQL Passwords

Stop the stack by running `docker-compose stop`.

When the containers came to a stop, run this command:

```
docker-compose run --rm --entrypoint '/bin/sh -c "gosu mysql mysqld --skip-grant-tables & sleep 10 && mysql -hlocalhost -uroot && exit 0"' mysql-openemail
```

### 1\. Find database name

```
# source openemail.conf
# docker-compose exec mysql-openemail mysql -u${DBUSER} -p${DBPASS} ${DBNAME}
MariaDB [(none)]> show databases;
+--------------------+
| Database           |
+--------------------+
| information_schema |
| openemail_database   | <=====
| mysql              |
| performance_schema |
+--------------------+
4 rows in set (0.00 sec)
```

### 2\. Reset one or more users

Both "password" and "authentication_string" exist. Currently "password" is used, but better set both.

```
MariaDB [(none)]> SELECT user FROM mysql.user;
+--------------+
| user         |
+--------------+
| openemail_user | <=====
| root         |
+--------------+
2 rows in set (0.00 sec)

MariaDB [(none)]> FLUSH PRIVILEGES;
MariaDB [(none)]> UPDATE mysql.user SET authentication_string = PASSWORD('gotr00t'), password = PASSWORD('gotr00t') WHERE User = 'root' AND Host = '%';
MariaDB [(none)]> UPDATE mysql.user SET authentication_string = PASSWORD('mookuh'), password = PASSWORD('mookuh') WHERE User = 'openemail' AND Host = '%';
MariaDB [(none)]> FLUSH PRIVILEGES;
```

## Remove Two-Factor Authentication

This works similar to resetting a MySQL password, now we do it from the host without connecting to the MySQL CLI:

```
source openemail.conf
docker-compose exec mysql-openemail mysql -u${DBUSER} -p${DBPASS} ${DBNAME} -e "DELETE FROM tfa WHERE username='YOUR_USERNAME';"
```

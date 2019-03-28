## Backup

```
cd /path/to/openemail-dockerized
source openemail.conf
DATE=$(date +"%Y%m%d_%H%M%S")
docker-compose exec -T mysql-openemail mysqldump --default-character-set=utf8mb4 -u${DBUSER} -p${DBPASS} ${DBNAME} > backup_${DBNAME}_${DATE}.sql
```

## Restore

!!! warning
    You should redirect the SQL dump without `docker-compose` to prevent parsing errors.

```
cd /path/to/openemail-dockerized
source openemail.conf
docker exec -i $(docker-compose ps -q mysql-openemail) mysql -u${DBUSER} -p${DBPASS} ${DBNAME} < backup_file.sql
```

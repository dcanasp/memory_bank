# theory

# practice
for mariadb inside a docker container
```sh
# Master
<INSIDE-CONTAINER>
mariadb -u root -p # password
CREATE USER 'replicator'@'%' IDENTIFIED BY 'replica';
GRANT REPLICATION SLAVE ON *.* TO 'replicator'@'%';
FLUSH PRIVILEGES;
SHOW MASTER STATUS;
exit
echo "[mysqld]" >> /etc/mysql/my.cnf
echo "server-id=1" >> /etc/mysql/my.cnf
echo "log_bin=mysql-bin" >> /etc/mysql/my.cnf
echo "binlog-do-db=my_app_development" >> /etc/mysql/my.cnf

mariadb -u root -p # password
SHOW MASTER STATUS;
exit
sudo docker restart <container-id>

# Slave
sudo docker network ls
sudo docker network inspect <the network name>
<INSIDE-CONTAINER>
mariadb -u root -p # password
STOP SLAVE;
CHANGE MASTER TO
    MASTER_HOST='<master-dns-name>', #change
    MASTER_USER='replicator',
    MASTER_PASSWORD='replica',
    MASTER_LOG_FILE='<file-from-show-status>', #change (this is the file name from the show master status, normally mysql-bin.000001 )
    MASTER_LOG_POS=<the-number-from-above>; #change same from above
START SLAVE;
SHOW SLAVE STATUS\G
exit
echo "[mysqld]" >> /etc/mysql/my.cnf
echo "server-id=2" >> /etc/mysql/my.cnf
exit
sudo docker restart <container-id>
```
postgres
```sh
# master
<INSIDE OF THE CONTAINER>
su - postgres
initdb -D /var/lib/postgresql/data
pg_ctl -o "-p 5490" start -D /var/lib/postgresql/data
psql -p 5490
CREATE USER replicator WITH REPLICATION ENCRYPTED PASSWORD 'replica';
\q

echo "listen_addresses = '*'" >> /var/lib/postgresql/data/postgresql.conf
echo "wal_level = replica" >> /var/lib/postgresql/data/postgresql.conf
echo "max_wal_senders = 10" >> /var/lib/postgresql/data/postgresql.conf
echo "wal_keep_size = 64" >> /var/lib/postgresql/data/postgresql.conf
echo "host replication replicator 0.0.0.0/0 md5" >> /var/lib/postgresql/data/pg_hba.conf
exit
pg_ctl restart -D /var/lib/postgresql/data
    #if db is not up
    su - postgres
    pg_ctl -o "-p 5490" start -D /var/lib/postgresql/data
# Slave
sudo docker network ls
sudo docker network inspect <the network name>
<INSIDE OF THE CONTAINER>
rm -rf /var/lib/postgresql/data/*
pg_basebackup -h <master-dns-name> -D /var/lib/postgresql/data -U replicator -p 5490 -P --wal-method=stream
touch /var/lib/postgresql/data/standby.signal
echo "primary_conninfo = 'host=<master-dns-name> port=5490 user=replicator password=replica'" >> /var/lib/postgresql/data/postgresql.conf
chown -R postgres:postgres /var/lib/postgresql/data
chmod -R 700 /var/lib/postgresql/data
su - postgres
pg_ctl -o "-p 5491" start -D /var/lib/postgresql/data

```
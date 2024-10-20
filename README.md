# lesson6

создал кластер и реплику на одной машине
```
sudo apt update && sudo DEBIAN_FRONTEND=noninteractive apt upgrade -y && sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt $(lsb_release -cs)-pgdg main" > /etc/apt/sources.list.d/pgdg.list' && wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add - && sudo apt-get update && sudo DEBIAN_FRONTEND=noninteractive apt -y install postgresql-16 unzip atop iotop

sudo pg_createcluster 16 main2

pg_lsclusters

Ver Cluster Port Status Owner    Data directory               Log file
16  main    5432 online postgres /var/lib/postgresql/16/main  /var/log/postgresql/postgresql-16-main.log
16  main2   5433 down   postgres /var/lib/postgresql/16/main2 /var/log/postgresql/postgresql-16-main2.log
root@ilinsinc:~# pg_lsclusters
```

```
 cat >> /etc/postgresql/16/main/postgresql.conf << EOL
listen_addresses = '192.168.1.2'
EOL
postgres@ilinsinc:/home/ilin.leonid2$ cd
postgres@ilinsinc:~$ cat >> /etc/postgresql/16/main/postgresql.conf << EOL
listen_addresses = '192.168.1.2'
EOL
postgres@ilinsinc:~$ cat >> /etc/postgresql/16/main/pg_hba.conf << EOL
host replication replicator 198.168.0.0/16 scram-sha-256
EOL
postgres@ilinsinc:~$ pg_ctlcluster 16 main stop && pg_ctlcluster 16 main start
Warning: stopping the cluster using pg_ctlcluster will mark the systemd unit as failed. Consider using systemctl:
  sudo systemctl stop postgresql@16-main
Warning: the cluster will not be running as a systemd service. Consider using systemctl:
  sudo systemctl start postgresql@16-main
```
Спустя 12 часов заработало)) пока не указал имя хоста внутренний ip

```
postgres@pgsinc:/home/ilin.leonid2$ pg_lsclusters
Ver Cluster Port Status        Owner    Data directory              Log file
16  main    5432 down,recovery postgres /var/lib/postgresql/16/main /var/log/postgresql/postgresql-16-main.log
```

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

# Database and Management

We can refer to my another configuration: [docker-databases-with-adminer](https://github.com/keer2345/docker-databases-with-adminer).

**Prepare:**
```sh
sudo mkdir /docker
sudo chmod 777 /docker
```

## Database
- Postgres
- MariaDB
- Redis

## Management
- pgAdmin4
- phpMyAdmin
- Adminer (optional)
- redisinsight

## Postgres
```sh
docker ps 

docker exec -it [Postgres Container ID] sh

# psql -U postgres
psql (17.4 (Debian 17.4-1.pgdg120+2))
Type "help" for help.

postgres=# \du
                             List of roles
 Role name |                         Attributes                         
-----------+------------------------------------------------------------
 postgres  | Superuser, Create role, Create DB, Replication, Bypass RLS

postgres=# \l
                                                    List of databases
   Name    |  Owner   | Encoding | Locale Provider |  Collate   |   Ctype    | Locale | ICU Rules |   Access privileges   
-----------+----------+----------+-----------------+------------+------------+--------+-----------+-----------------------
 postgres  | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | 
 template0 | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | =c/postgres          +
           |          |          |                 |            |            |        |           | postgres=CTc/postgres
 template1 | postgres | UTF8     | libc            | en_US.utf8 | en_US.utf8 |        |           | =c/postgres          +
           |          |          |                 |            |            |        |           | postgres=CTc/postgres
(3 rows)

postgres=# create database "test";
CREATE DATABASE
```

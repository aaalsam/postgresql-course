anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % nano docker-compose.yaml
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker-compose up -d
WARN[0000] /Users/anastasia/Desktop/wb/Курс PostgreSQL/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Running 15/15
 ✔ postgres Pulled                                                 12.6s 
   ✔ 8c21e9d8fa8c Download complete                                 0.9s 
   ✔ 77b1b7588421 Download complete                                 0.5s 
   ✔ 2c6810bb3d75 Download complete                                 0.7s 
   ✔ f45b4b1e09b9 Download complete                                 0.7s 
   ✔ 1cfbe96df98f Download complete                                 1.1s 
   ✔ 774c54d2d309 Download complete                                 0.6s 
   ✔ 434de25e58a4 Download complete                                 0.8s 
   ✔ cf8078a8a245 Download complete                                 1.7s 
   ✔ 551bc275c65f Download complete                                 7.0s 
   ✔ 1655e767f751 Download complete                                 1.2s 
   ✔ 7b8417b4134b Download complete                                 0.8s 
   ✔ a1dedce88ca1 Download complete                                 0.9s 
   ✔ d51c377d94da Download complete                                 4.5s 
   ✔ 405f36104e57 Download complete                                 1.8s 
[+] Running 3/3
 ✔ Network postgresql_default         Created                       0.0s 
 ✔ Volume "postgresql_postgres-data"  Created                       0.0s 
 ✔ Container my-postgres              St...                         0.5s 
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % wget https://storage.googleapis.com/thaibus/thai_small.tar.gz
tar -xf thai_small.tar.gz

--2025-03-16 21:20:44--  https://storage.googleapis.com/thaibus/thai_small.tar.gz
Распознаётся storage.googleapis.com (storage.googleapis.com)… 142.250.74.91, 142.250.74.27, 142.250.74.187, ...
Подключение к storage.googleapis.com (storage.googleapis.com)|142.250.74.91|:443... соединение установлено.
HTTP-запрос отправлен. Ожидание ответа… 200 OK
Длина: 84252589 (80M) [application/x-gzip]
Сохранение в: «thai_small.tar.gz»

thai_small.tar.gz     100%[=======================>]  80,35M  1,56MB/s    за 39s     

2025-03-16 21:21:23 (2,07 MB/s) - «thai_small.tar.gz» сохранён [84252589/84252589]
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker cp thai.sql my-postgres:/thai.sql

Successfully copied 307MB to my-postgres:/thai.sql
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker exec -it my-postgres createdb -U testuser thai


What's next:
    Try Docker Debug for seamless, persistent debugging tools in any container or image → docker debug my-postgres
    Learn more at https://docs.docker.com/go/debug-cli/
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker exec -i my-postgres psql -U testuser -d thai < thai.sql

SET
SET
SET
SET
SET
 set_config 
------------
 
(1 row)

SET
SET
SET
SET
ERROR:  database "thai" already exists
ERROR:  role "postgres" does not exist
You are now connected to database "thai" as user "testuser".
SET
SET
SET
SET
SET
 set_config 
------------
 
(1 row)

SET
SET
SET
SET
CREATE SCHEMA
ERROR:  role "postgres" does not exist
SET
SET
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
CREATE TABLE
ERROR:  role "postgres" does not exist
CREATE SEQUENCE
ERROR:  role "postgres" does not exist
ALTER SEQUENCE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
COPY 5
COPY 60
COPY 10
COPY 111
COPY 109
COPY 144000
COPY 1440
COPY 200
COPY 3
COPY 5185505
 setval 
--------
      1
(1 row)

 setval 
--------
     60
(1 row)

 setval 
--------
      1
(1 row)

 setval 
--------
 144000
(1 row)

 setval 
--------
   1440
(1 row)

 setval 
--------
    200
(1 row)

 setval 
--------
      1
(1 row)

 setval  
---------
 5185505
(1 row)

ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
ALTER TABLE
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker exec -it my-postgres psql -U testuser -d thai

psql (17.4 (Debian 17.4-1.pgdg120+2))
Type "help" for help.
thai=# \dn
      List of schemas
  Name  |       Owner       
--------+-------------------
 book   | testuser
 public | pg_database_owner
(2 rows)

thai=# SET search_path TO book;
SET
thai=# \dt
            List of relations
 Schema |     Name     | Type  |  Owner   
--------+--------------+-------+----------
 book   | bus          | table | testuser
 book   | busroute     | table | testuser
 book   | busstation   | table | testuser
 book   | fam          | table | testuser
 book   | nam          | table | testuser
 book   | ride         | table | testuser
 book   | schedule     | table | testuser
 book   | seat         | table | testuser
 book   | seatcategory | table | testuser
 book   | tickets      | table | testuser
(10 rows)

thai=# select count(*) from book.tickets;
  count  
---------
 5185505
(1 row)
thai=# \q
anastasia@MacBook-Pro-Anastasia Курс PostgreSQL % docker-compose stop 
WARN[0000] /Users/anastasia/Desktop/wb/Курс PostgreSQL/docker-compose.yaml: the attribute `version` is obsolete, it will be ignored, please remove it to avoid potential confusion 
[+] Stopping 1/1
 ✔ Container my-postgres  Stopped                                                0.1s 

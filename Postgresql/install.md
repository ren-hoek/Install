Following repo setup from 
https://wiki.postgresql.org/wiki/Apt#Documentation
and pg setup from:
https://www.codeproject.com/Articles/898303/Installing-and-Configuring-PostgreSQL-on-Linux-Min

sudo sh -c 'echo "deb http://apt.postgresql.org/pub/repos/apt/ xenial-pgdg main" > /etc/apt/sources.list.d/pgdg.list'
sudo apt-get install wget ca-certificates
wget --quiet -O - https://www.postgresql.org/media/keys/ACCC4CF8.asc | sudo apt-key add -
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install postgresql-9.5 pgadmin3
su -
su - postgres
psql
postgres=# CREATE USER gavin
postgres-# WITH SUPERUSER CREATEDB CREATEROLE
postgres-# PASSWORD '*******';
postgres=# \q
exit
exit
psql postgres
postgres=# CREATE DATABASE test_db WITH OWNER gavin;
postgres=# \connect test_db;
test_db=# CREATE TABLE products (id SERIAL PRIMARY KEY, name TEXT);
test_db=# INSERT INTO products (name) VALUES ('Brass Widgets');
test_db=# SELECT * FROM products;

psql postgres
postgres=# CREATE USER r PASSWORD 'r';
postgres=# CREATE DATABASE r WITH OWNER r;

pgadmin3

## Installing RPostgreSQL
sudo apt-get install libpq-dev
sudo apt-get install gfortran

## In R
install.packages('RPostgreSQL', dependencies = TRUE)
require("RPostgreSQL")

see RPostgreSQL.R to see how to use with src_postgres in dplyr

# Influx DB Command Line Interface Commands

### Getting Started

```bash
# install influxdb client
$ sudo apt-get install influxdb-client

# make sure you have influxdb installed and then start the server
$ sudo service InfluxDB start

# start the influxdb client
$ influx
```

### `show databases`

shows a list of all the databases on the server

### `create database <new database name>`

creates a new database on the server with the given name

### `use <database name>`

switches current database to the given database so you can view and add measurements

### `show measurements`

shows a list of all the different measurements being recorded in the active database

### `insert <measurement>,key1=value1 key2=value2 ...`

inserts a record into the database. `measurement` specifies what measurement the record is which is followed by a series of key value pairs of which there is no limit

### `<SQL query>`

use can use any SQL query to access specific data

```sql
select * from <measurement> where <key>=<value>
```

### `drop <type> <type name>`

used to delete series, measurements, or databases from the server. this works similar to the sql drop command

```sql
drop measurement cpu_usage
```

### `show series`

shows time series of all the measurements on the database


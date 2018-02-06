# MariaDB Docker images for Docksal

These MariaDB images are derived from the stock `mariadb` available at [Docker Hub](https://hub.docker.com/_/mariadb/).
 The files `default.cnf` and `docker-entrypoint.sh` contain several modifications.

## Available versions:

- `mariadb-5.5`
- `mariadb-10.0`
- `mariadb-10.1`
- `mariadb-10.2`
- `mariadb-10.3`

## How to:

If you're already using predefined Docksal stack, you can easily add MariaDB to it.

1.) Choose the version of the MariaDB (5.5, 10.0, 10.1, 10.2, 10.3) and add it 
inside `docksal.env` file inside `.docksal` directory (under your project root directory).

2.) Make the `docksal.yml` file and instruct Docksal to use the chosen MariaDB version. For example:

`docksal.env` (change DB_IMAGE line)

```
DB_IMAGE='ilakic/mariadb-docksal:mariadb-10.1'
```

`docksal.yml` 

```yml
# This is a library of preconfigured services for Docksal.
# To use any service extend it from this file located at ${HOME}/.docksal/stacks/services.yml.
# See ${HOME}/.docksal/stacks/default.yml for a basic LAMP stack extending from web, db and cli services in this file.

version: "2.1"

services:
  # DB
  db:
    hostname: db
    image: ${DB_IMAGE:-ilakic/mariadb-docksal:mariadb-10.1}
```

In `docksal.yml` we just copied `db` services from default Docksal stack and made a small modification for `image`.

This way, you'll still going to use stack that you're already been using and overwrite just `db` part of the stack configuration.

More about that [here](http://docksal.readthedocs.io/en/master/advanced/stack-config/).

## **IMPORTANT!**
**Be careful** if you already have project which uses MySQL database. The same goes if you are just switching from MySQL to MariaDB in your Docksal dev environment. Migrations from one database to another can be tricky, so **make sure you make a backup copy of your database** first.
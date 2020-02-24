# todolist deploy

## Setup

Create env.ini file.  

```ini
[System]
ip = 0.0.0.0
port = 5000
auth_key = secret key

[Database]
host = db
port = 5432
user = postgres
password = password
dbname = todo_database
```

## Run

```shell
$ docker-compose up -d

# init database if first use, create database and table, reference README.md of backend
$ docker exec -it todolist-deploy_db_1 psql -U postgres
```

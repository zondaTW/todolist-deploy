# todolist deploy

## Setup

Create env.ini and nginx.conf file.  

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

```nginx
events {
    worker_connections  1024;
}


http {
    server {
		listen 80;
		server_name localhost;
		
		location / {
			root /usr/share/nginx/html/;
			index index.html;
		
			location ~ \.css {
				add_header Content-Type text/css;
			}
		
			location ~ \.js {
				add_header Content-Type application/x-javascript;
			}
		}
		
		location /login {
			if ($request_method = POST) {
				proxy_pass http://backend:5000;
			}
			if ($request_method = GET) {
				return 301 /;
			}
		}
	
		location ~ ^/(api|auth)/ {
			proxy_pass http://backend:5000;
		}
	}
}
```

### frontend setup

create .env.production.local file.

```txt
VUE_APP_API_BASE_URL=
```

```shell
$ cd frontend
$ npm install
$ npm run build
```


## Run

```shell
$ docker-compose up -d

# init database if first use, create database and table, reference README.md of backend
$ docker exec -it todolist-deploy_db_1 psql -U postgres
```

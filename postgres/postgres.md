## Postgres

### 1.安装

#### 1.1docker启动postgres
```
docker run -it -d --name docker-postgresql \ 
  -p 5432:5432 \
  -restart always \ 
  -e TZ=Asia/Shanghai \ 
  -e POSTGRES_USER=postgres \ 
  -e POSTGRES_PASSWORD=12345678 \ 
  -e POSTGRES_DB=postgres \ 
  -v /data/postgres/data:/var/lib/postgresql/data \ 
  -v /data/postgres/conf/postgres.conf:/etc/postgresql/postgresql.conf \ 
  postgres:16.2
```

#### 1.2用docker-compose启动postgres
```
docker-compose -f docker-compose_postgres.yml up -d
```

### 2.安装postgis、pgdebugger(pldbapi)插件
apt-get update
apt-get install -y postgresql-16-postgis-3 postgresql-16-postgis-3-dbgsym postgresql-16-postgis-3-scripts
apt-get install postgresql-16-pldebugger

### 3.进入数据库启动插件
CREATE EXTENSION postgis;
CREATE EXTENSION pldbgapi;

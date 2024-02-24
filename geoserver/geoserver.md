## Postgres

### 1.安装

#### 1.1docker启动geoserver
```
docker run -it -d -p 8081:8080 --name geoserver \
  -restart always  \
  -v /data/geoserver/libs:/opt/additional_libs  \
  -v /data/geoserver/data:/opt/geoserver_data  \
  --env INSTALL_EXTENSIONS=true \
  --env STABLE_EXTENSIONS="importer,printing,monitor,params-extractor,css,vectortiles" \
  docker.osgeo.org/geoserver:2.22.5
```

#### 1.2用docker-compose启动geoserver
```
docker-compose -f docker-compose_geoserver.yml up -d
```

### 2.安装geomesa、hbase插件

1.将jars里的jar包放到/data/geoserver/libs/目录下
2.进入geoserver容器，将/opt/additional_libs下的jar包复制到/opt/apache-tomcat-9.0.75/webapps/geoserver/WEB-INF/lib下
3.退出容器，重新启动容器

PS:geomesa-hbase_2.12-4.0.4

### 3.其他
默认用户名geoserver，密码geoserver
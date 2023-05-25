### 单机版

```
docker run --name vm_dgraph -d -p "8080:8080" -p "9080:9080" -p "7000:8080" -p "8000:8000" -p "6080:6080" -v /data/container/dgraph:/dgraph dgraph/standalone:latest
```

### 备份
    1.进入docker容器内部执行命令
```
curl -Ss -H "Content-Type: application/json" http://<IP_ADDRESS>:<PORT>/admin -XPOST -d '{ "query": "mutation { export(input: {format: \"json\"}) { response { code message } }}" }'
```
    PS: IP_ADDRESS需要在docker-compose.yml中whitelist里，本机也可以用localhost
        PORT端口缺省是8080
        json可以改为rdf
    
    2.在容器外部执行命令
```
docker exec -it <alpha容器ID> bash -c "curl -Ss -H \"Content-Type: application/json\" http://<IP_ADDRESS>:<PORT>/admin -XPOST -d '{ \"query\": \"mutation { export(input: {format: \\\"json\\\"}) { response { code message } }}\" }'"
```
    PS：容器ID，单机是容器ID，非单机是alpha容器ID 
        IP_ADDRESS需要在docker-compose.yml中whitelist里，本机也可以用localhost
        PORT端口缺省是8080
        json可以改为rdf
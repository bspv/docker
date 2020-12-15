## Node

1.拉取node你镜像
```
    docker pull node
```

2.npm install
```
docker run -it --rm -v "$(pwd)":/app -v /data/container/node/logs:/root/.npm/_logs/ -w /app node npm install --legacy-peer-deps
```
    注：
        -v "$(pwd)":/app 将当前目录挂载到容器的/app下
        -v /data/container/node/logs:/root/.npm/_logs/ 将npm日志挂载到宿主机
        -w /app 指定工作路径
        node 镜像名称
        npm install --legacy-peer-deps 打包命令

3.npm run build
```
docker run -it --rm -v "$(pwd)":/app -v /data/container/node/logs:/root/.npm/_logs/ -w /app node npm run build:test
```
    注：
        -v "$(pwd)":/app 将当前目录挂载到容器的/app下
        -v /data/container/node/logs:/root/.npm/_logs/ 将npm日志挂载到宿主机
        -w /app 指定工作路径
        node 镜像名称
        npm run build:dev 运行
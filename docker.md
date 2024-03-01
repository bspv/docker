## Docker

## 1.安装docker
    curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

    systemctl start docker # 启动docker

    systemctl enable docker.service # 开机启动

    docker --version # 查看版本

## 2.[安装docker-compose](https://docs.docker.com/compose/install/)

### 2.1命令行下载
    sudo curl -L "https://github.com/docker/compose/releases/download/$(改成具体版本号)/docker-compose-$(uname -s | awk '{print tolower($0)}')-$(uname -m)" -o /usr/local/bin/docker-compose
### 2.2git下载文件
    进入https://github.com/docker/compose/releases/，找到linux-x86_64版本下载
    然后上传对应机器，再把docker-compose-linux-x86_64改为docker-compose，再移动到/usr/local/bin/目录下

### 2.3增加权限，建软连接
    sudo chmod +x /usr/local/bin/docker-compose

    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

    docker-compose --version

## 3.其他
    1.one_pc.yml是将所有中间件安装在一台机器上，需要将yml中192.168.0.1修改为具体的IP
    2.docker-compose_{num}.yml是安装在3台机器上，需要修改192.168.0.1-3改为具体的IP
    3.如果分开多个docker-compose_*.yml的话，放置到不同文件夹里，或者放置同一个目录下启动的时候用-p name来指定项目名字


### 4.使用
    1.查看docker容器的实时CPU、内存信息
        docker stats --format "table {{.Name}}\t{{.CPUPerc}}\t{{.MemUsage}}" ${containerId}
    2.查看docker挂载的源目录和目标目录信息
        docker inspect --format "{{range .Mounts}}{{println .Source}}{{end}}" ${containerId}
        docker inspect --format "{{range .Mounts}}{{println .Destination}}{{end}}" ${containerId}


### 5.镜像导出导入
    1.镜像导出
        docker save -o /data/dgraph.tar dgraph/standalone:v23.0.0 dgraph/ratel:v21.12.0
    2.镜像导入
        docker load < /data/dgraph.tar

### [6.容器配置更改](https://blog.csdn.net/lishuoboy/article/details/130174200)
    6.1) 查找docker路径、容器id
    docker info | grep 'Docker Root' #docker路径
    docker ps -a --no-trunc | grep  容器名 #查找容器信息，容器id等
    6.2) 停止容器
    docker stop $containerId
    6.3) 修改配置文件
    vim ${Docker Root}/containers/${containerId}/config.v2.json
    vim ${Docker Root}/containers/${containerId}/config.json
    6.4) 重启docker服务
    sudo systemctl stop docker.socket
    sudo systemctl stop docker
    sudo systemctl start docker

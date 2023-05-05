## Docker

## 1.安装docker
    curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

    systemctl start docker # 启动docker

    systemctl enable docker.service # 开机启动

    docker --version # 查看版本

## 2.[安装docker-compose](https://docs.docker.com/compose/install/)
    sudo curl -L "https://github.com/docker/compose/releases/download/Latest/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

    sudo chmod +x /usr/local/bin/docker-compose

    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

    docker-compose --version

## 3.其他
    1.one_pc.yml是将所有中间件安装在一台机器上，需要将yml中192.168.0.1修改为具体的IP
    2.docker-compose_{num}.yml是安装在3台机器上，需要修改192.168.0.1-3改为具体的IP
    3.如果分开多个docker-compose_*.yml的话，放置到不同文件夹里，或者放置同一个目录下启动的时候用-p name来指定项目名字
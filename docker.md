## Docker

## 1.安装docker
    curl -fsSL https://get.docker.com -o get-docker.sh && sh get-docker.sh

    查看版本
    docker --version

## 2.启动docker
    systemctl start docker

    systemctl enable docker.service


## 3.[安装docker-compose](https://docs.docker.com/compose/install/)
    sudo curl -L "https://github.com/docker/compose/releases/download/1.27.4/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-compose

    sudo chmod +x /usr/local/bin/docker-compose

    sudo ln -s /usr/local/bin/docker-compose /usr/bin/docker-compose

    docker-compose --version


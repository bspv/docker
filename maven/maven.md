## Maven

1.拉取Maven你镜像
    docker pull maven:3.6.3-jdk-8-slim
2.创建一个公共数据卷maven-repo
    docker volume create --name maven-repo
3.1指定settings.xml和仓库位置，直接打包
```
    docker run -it --rm -v "$(pwd)":/app -w /app -v /data/maven/settings.xml:/usr/share/maven/ref/settings.xml -v maven-repo:/usr/share/maven/ref/repository maven:3.6.3-jdk-8-slim mvn clean package -pl module-name -am -P test  -Dmaven.test.skip=true
```
    注：
        -v "$(pwd)":/app 将当前目录挂载到容器的/app下
        -v /data/maven/settings.xml:/usr/share/maven/ref/settings.xml 将宿主机的settings.xml挂载到容器内对应的settings.xml文件
        -v maven-repo:/usr/share/maven/ref/repository 将公共卷挂载到容器内maven仓库
        maven:3.6.3-jdk-8-slim 镜像名称
        mvn clean package -pl module-name -am -P test  -Dmaven.test.skip=true 打包命令
3.2.1在公共卷maven-repo(路径：/var/lib/docker/volumes/maven-repo)下放置settings.xml文件
3.2.2在项目根目录下执行编译命令
```
    docker run -it --rm -v "$(pwd)":/app -w /app -v maven-repo:/usr/share/maven/ref maven:3.6.3-jdk-8-slim mvn clean package -pl module-name -am -P test  -Dmaven.test.skip=true
```
    注：
        -v "$(pwd)":/app 将当前目录挂载到容器的/app下
        -v maven-repo:/usr/share/maven/ref 将公共卷挂载到容器内maven仓库上一级，即将settings.xml同步到容器内，同时将maven仓库同步到公共卷中
        maven:3.6.3-jdk-8-slim 镜像名称
        mvn clean package -pl module-name -am -P test  -Dmaven.test.skip=true 打包命令


mvn clean package -pl module-name -am -P test  -Dmaven.test.skip=true
相当于
mvn clean install -Dmaven.test.skip=true
mvn -f ./module-name/pom.xml clean package -P test -Dmaven.test.skip=true
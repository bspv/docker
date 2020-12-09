## storm

```
docker run --network docker-network --link nimbus:nimbus -it --rm -v $(pwd)/analysis.jar:/usr/app/analysis.jar -v /data/container/storm/nimbus/logs:/logs -e "TZ=Asia/Shanghai" -w /usr/app/ storm storm jar analysis.jar com.bazzi.analysis.AnalysisProcessor analysis-topology
```
    --network docker-network docker环境的网络
    --link nimbus:nimbus   链接到nimbus，冒号前面的是docker容器对应的nimbus名字
    -it 以交互方式启动
    --rm 删除
    -v $(pwd)/analysis.jar:/usr/app/analysis.jar 将当前路径下的analysis.jar挂载到容器内/usr/app/analysis.jar
    -v /data/container/storm/nimbus/logs:/logs 把容器内/logs目录挂载到/data/container/storm/nimbus/logs，同步日志到宿主机
    -e "TZ=Asia/Shanghai" 设置环境变量，这里是设置时区
    -w /usr/app/ 指定容器内工作目录
    storm storm jar analysis.jar com.bazzi.analysis.AnalysisProcessor analysis-topology 启动topology

```
docker run --network docker-network --link nimbus:nimbus -it --rm -v /data/container/storm/nimbus/logs:/logs -e "TZ=Asia/Shanghai" storm storm kill analysis-topology
```
    --network docker-network docker环境的网络
    --link nimbus:nimbus   链接到nimbus，冒号前面的是docker容器对应的nimbus名字
    -it 以交互方式启动
    --rm 删除
    -v /data/container/storm/nimbus/logs:/logs 把容器内/logs目录挂载到/data/container/storm/nimbus/logs，同步日志到宿主机
    -e "TZ=Asia/Shanghai" 设置环境变量，这里是设置时区
    storm storm kill analysis-topology 关闭topology


注：多台机器集群需要将storm.yaml放到docker-compose.yml挂载目录，以替换原有storm.yaml
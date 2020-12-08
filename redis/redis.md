## [Redis](https://blog.csdn.net/wzhzzzz/article/details/100771906)

## 1.one_pc版本
1.添加配置文件到yml设置的路径中
2.docker-compose -f docker-compose_redis.yml up -d启动
3.docker exec -it redis-7001 /bin/bash进入容器
4.进入/usr/local/bin执行创建集群命令
    redis-cli -a 123456 --cluster create 192.168.0.1:7001 192.168.0.1:7002 192.168.0.1:7003 192.168.0.1:7004 192.168.0.1:7005 192.168.0.1:7006 --cluster-replicas 1
5.进行验证
    进入redis集群：redis-cli -a 123456 -c -h 192.168.0.1 -p 7001
    执行 cluster info 或者cluster nodes
6.退出容器

## 2.cluster版本
1.将redis-7001.conf、redis-7004.conf、docker-compose_redis_1.yml放在机器1上启动
  将redis-7002.conf、redis-7005.conf、docker-compose_redis_2.yml放在机器2上启动
  将redis-7003.conf、redis-7006.conf、docker-compose_redis_3.yml放在机器3上启动
  注：redis-700*.conf中需先修改IP地址
2.docker exec -it redis-7001 /bin/bash进入容器
3.进入/usr/local/bin执行创建集群命令
    redis-cli -a 123456 --cluster create 192.168.0.1:7001 192.168.0.2:7002 192.168.0.3:7003 192.168.0.1:7004 192.168.0.2:7005 192.168.0.3:7006 --cluster-replicas 1
4.进行验证
    进入redis集群：redis-cli -a 123456 -c -h 192.168.0.1 -p 7001
    执行 cluster info 或者cluster nodes
5.退出容器
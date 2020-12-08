## kafka

1.启动kafka
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-server-start.sh -daemon /usr/local/kafka/kafka_2.13-2.6.0/config/server.properties &
```

2.查看Topic
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --list --zookeeper 192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181
```

3.创建Topic
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --create --topic topic_log_detail --zookeeper 192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181 --config max.message.bytes=12800000 --config flush.messages=1 --partitions 4 --replication-factor 1
```

4.查看Topic的分区和副本情况
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --describe --zookeeper 192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181  --topic topic_log_detail
```

5.修改topic的partition数量（只能增加不能减少）
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --alter --zookeeper 192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181 --partitions 4 --topic topic_log_detail
```

6.查看topic消费到的offset
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-run-class.sh kafka.tools.GetOffsetShell --broker-list 192.168.0.1:9092,192.168.0.2:9092,192.168.0.3:9092 --topic topic_log_detail --time -1
```

7.删除Topic
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-topics.sh --delete --zookeeper 192.168.0.1:2181,192.168.0.2:2181,192.168.0.3:2181 --topic topic_log_detail
```

8.消息消费
```
/usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-console-consumer.sh --bootstrap-server 192.168.0.1:9092,192.168.0.2:9092,192.168.0.3:9092 --topic topic_log_detail
```

9.以后台方式，像kafka发送消息，发送日志保存到当前位置的kafka_test.log中
```
nohup /usr/local/kafka/kafka_2.13-2.6.0/bin/kafka-producer-perf-test.sh  --topic topic_log_detail  --print-metrics --payload-file /data/bin/3.txt --num-records 2000 --throughput 200  --producer-props bootstrap.servers=192.168.0.1:9092,192.168.0.2:9092,192.168.0.3:9092 > kafka_test.log  2>&1 &
```
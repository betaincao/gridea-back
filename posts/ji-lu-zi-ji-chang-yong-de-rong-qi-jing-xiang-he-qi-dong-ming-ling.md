---
title: '记录自己常用的容器镜像和启动命令'
date: 2022-06-20 11:10:20
tags: [docker]
published: true
hideInList: false
feature: 
isTop: false
---
#### mysql
```sh
docker run -p 3306:3306 --name mysql \
-v /usr/local/docker/mysql/conf:/etc/mysql \
-v /usr/local/docker/mysql/logs:/var/log/mysql \
-v /usr/local/docker/mysql/data:/var/lib/mysql \
-e MYSQL_ROOT_PASSWORD=123456 \
-d mysql:5.7
```

#### phpmyadmin
```sh
docker run --name phpmyadmin -d --link mysql -e PMA_HOST="mysql" -p 6061:80 phpmyadmin/phpmyadmin
```

#### elasticsearch
```sh
docker run -e  -d -p 9200:9200 -p 9300:9300 -v ${ES_SINGLE}/config/es-single.yml:/usr/share/elasticsearch/config/elasticsearch.yml -v ${ES_SINGLE}/data:/usr/share/elasticsearch/data --name es-single elasticsearch:7.6.2
```

#### redis
```sh
docker run --name redis -d -p 6380:6379 redis
```

#### prometheus
```sh
docker run  -d   -p 10050:9090   -v /opt/prometheus/prometheus.yml:/etc/prometheus/prometheus.yml    prom/prometheus
```

#### grafana
```sh
docker run -d   -p 10051:3000   --name=grafana   -e "GF_SERVER_ROOT_URL=http://grafana.server.name"   -e "GF_SECURITY_ADMIN_PASSWORD=admin"   grafana/grafana
```

#### kafka
```sh
docker run -d --name kafka -p 15672:9092 -e KAFKA_BROKER_ID=0 -e KAFKA_ZOOKEEPER_CONNECT=zookeeper:5672 --link zookeeper -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://47.93.185.66:15672 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:15672 -t wurstmeister/kafka
```

#### http文件服务
```sh
docker run -it --rm -p 7000:8000 -v $PWD:/app/public --name gohttpserver -d bushinvren1986/mygohttpserver:v1 --upload --delete
```
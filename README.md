# mysql-pxc
Percona XtraDB Cluster Docker 集群方案

#### 构建 build
      构建master
            docker build -t xtradb:master .
      构建slave
            docker build -t xtradb:slave .
#### 运行 run
      docker run -d --name xtradbnode1 -p 3306:3306 xtradb:master /usr/bin/mysqld_safe
      docker run -d --name xtradbnode2 -p 13306:3306 --link xtradbnode1:node1 xtradb:slave /usr/bin/mysqld_safe
      docker run -d --name xtradbnode3 -p 23306:3306--link xtradbnode1:node1 xtradb:slave /usr/bin/mysqld_safe
#### 测试 test
      通过mysql命定行查看是否成功
      
      mysql$:show global status like 'wsrep_cluster_size';
####  方案来自：
      http://www.oschina.net/translate/percona-xtradb-cluster-how-to-run-a-2-node-cluster-on-a-single-server

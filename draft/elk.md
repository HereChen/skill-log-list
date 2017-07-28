# ELK

ElasticSearch, Logstash, Kinbana, X-Pack

## 环境

**jdk**

安装 `jdk1.8.0_131` 到 `/usr/local/`.

```bash
vim /etc/profile
# export JAVA_HOME=/usr/local/java/jdk1.8.0_131
# export CLASSPATH=.:$JAVA_HOME/lib/tools.jar:$JAVA_HOME/lib/dt.jar
# export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH

source /etc/profile
java -version
```

## ElasticSearch

1. 不能在 root 下启动.
2. IP 访问需要设置.

**安装配置**

```bash
cd /usr/local/
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.5.0.tar.gz
tar -xvzf elasticsearch-5.5.0.tar.gz

# 添加 elastic 用户组, root 下无法安装
groupadd elastic
useradd elastic -g elastic -p elasticsearch-5.5.0
chown -R elastic:elastic elasticsearch-5.5.0
su elastic

# vim elasticsearch
# ES_JAVA_OPTS="-Des.insecure.allow.root=true"
./elasticsearch-5.5.0/bin/elasticsearch

# 通过 IP 访问
vim elasticsearch-5.5.0/config/elasticsearch.yml
# network.host: 0.0.0.0
# http.port: 9200
```

**防火墙设置**

```bash
vim /etc/selinux/config
# SELINUX=disabled

yum install firewalld firewall-config
systemctl start firewalld.service
systemctl enable firewalld.service
systemctl status firewalld.service

firewall-cmd --permanent --add-port={9200/tcp,9300/tcp}
firewall-cmd --reload
firewall-cmd --state
firewall-cmd --list-all
```

**访问**

```bash
curl http://IP:9200
curl http://localhost:9200
```

**问题**

```bash
# max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]
su root
vim /etc/sysctl.conf 
# vm.max_map_count=655360
sysctl -p

# [1]: max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]
su root
vim /etc/security/limits.conf
# * soft nofile 65536
# * hard nofile 131072
# * soft nproc 2048
# * hard nproc 4096
```

**其他**

```bash
# 后台启动
./elasticsearch -d

systemctl daemon-reload #重启加载systemd
systemctl enable elasticsearch.service #自启动elasticsearch
systemctl start elasticsearch.service #启动elasticsearch
systemctl stop elasticsearch.service #停止elasticsearch
```

**参考**

- 安装: [Elasticsearch Reference [5.5] » Getting Started » Installation](https://www.elastic.co/guide/en/elasticsearch/reference/current/_installation.html)
- 安装参考: [Elasticsearch在Centos 7上的安装与配置](https://www.biaodianfu.com/centos-7-install-elasticsearch.html)
- 问题参考: [Elasticsearch5.0 安装问题集锦](https://www.cnblogs.com/sloveling/p/elasticsearch.html)

## Kinbana

**安装**

```bash
wget https://artifacts.elastic.co/downloads/kibana/kibana-5.5.0-linux-x86_64.tar.gz
tar -xvzf kibana-5.5.0-linux-x86_64.tar.gz
mv kibana-5.5.0-linux-x86_64 /usr/local/
cd /usr/local/

vim kibana-5.5.0-linux-x86_64/conf/kibana.yml
# server.host : "0.0.0.0"

nohup kibana-5.5.0-linux-x86_64/bin/kibana &
```

**防火墙设置**

```bash
firewall-cmd --permanent --add-port={5601/tcp}
firewall-cmd --reload
```

**参考**

- 安装: [Kibana User Guide [5.5] » Set Up Kibana » Installing Kibana](https://www.elastic.co/guide/en/kibana/current/targz.html)

## Logstash

**安装**

```bash
cd /opt/
wget https://artifacts.elastic.co/downloads/logstash/logstash-5.5.0.tar.gz

tar -xvzf logstash-5.5.0.tar.gz
mv logstash-5.5.0 /usr/local/
```

## x-pack

```bash
# offline install
cd /opt/
wget https://artifacts.elastic.co/downloads/packs/x-pack/x-pack-5.5.0.zip

/usr/local/elasticsearch-5.5.0/bin/elasticsearch-plugin install file:///opt/x-pack-5.5.0.zip
/usr/local/kibana-5.5.0-linux-x86_64/bin/kibana-plugin install file:///opt/x-pack-5.5.0.zip
/usr/local/logstash-5.5.0/bin/logstash-plugin install file:///opt/x-pack-5.5.0.zip
```

**参考**

- [Install X-Pack](https://www.elastic.co/guide/en/x-pack/current/installing-xpack.html)

## xx

- elasticsearch 登录: elastic/changeme

## 参考

- [搭建日志管理系统](https://beyondalbert.com/fan-yi-wen-da-jian-ri-zhi-guan-li-xi-tong/)
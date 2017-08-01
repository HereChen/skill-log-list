# ELK

- CentOS 7.3
- jdk1.8
- ElasticSearch 5.5.0
- Logstash 5.5.0
- Kinbana 5.5.0
- X-Pack 5.5.0
- Filebeat 5.5.0

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

**安装**

```bash
cd /usr/local/
wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-5.5.0.tar.gz
tar -xvzf elasticsearch-5.5.0.tar.gz
mv elasticsearch-5.5.0 /usr/local/
```

**添加 elastic 用户组**

添加 elastic 用户组, root 下无法安装运行.

```bash
groupadd elastic
useradd elastic -g elastic -p elasticsearch-5.5.0
chown -R elastic:elastic elasticsearch-5.5.0
su elastic
```

**配置(elasticsearch.yml)**

```yaml
# vim /usr/local/elasticsearch-5.5.0/config/elasticsearch.yml
network.host: 0.0.0.0
http.port: 9200
```

**防火墙设置**

```conf
# vim /etc/selinux/config
SELINUX=disabled
```

```bash
yum install firewalld firewall-config
systemctl start firewalld.service
systemctl enable firewalld.service
systemctl status firewalld.service

firewall-cmd --permanent --add-port={9200/tcp,9300/tcp}
firewall-cmd --reload
firewall-cmd --state
firewall-cmd --list-all
```

**启动**

```bash
su elastic
# 后台启动
./usr/local/elasticsearch-5.5.0/bin/elasticsearch -d
```

**访问**

```bash
curl http://IP:9200
curl http://localhost:9200
```

**其他**

```bash
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
```

**配置(kibana.yml)**

```yaml
# vim /usr/local/kibana-5.5.0-linux-x86_64/conf/kibana.yml
server.host : "0.0.0.0"
```

**防火墙设置**

```bash
firewall-cmd --permanent --add-port=5601/tcp
firewall-cmd --reload
```

**启动**

```bash
nohup kibana-5.5.0-linux-x86_64/bin/kibana &
```

**访问**

```bash
curl http://localhost:5601
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

**配置 SSL**

```yaml
# vim /etc/pki/tls/openssl.cnf
# 找到 [v3_ca] 段，添加 subjectAltName 一行
[v3_ca]
subjectAltName = IP: logstash_server_ip
```

```bash
openssl req -config /etc/pki/tls/openssl.cnf -x509 -days 2650 -batch -nodes -newkey rsa:2048 -keyout /etc/pki/tls/private/logstash.key -out /etc/pki/tls/certs/logstash.crt

# 复制到 filebeat 服务器
scp /etc/pki/tls/certs/logstash.crt 192.168.100.146:/etc/pki/tls/certs/
```

**配置 logstash (filebeat.conf)**

```yaml
# mkdir /usr/local/logstash-5.5.0/conf/
# touch /usr/local/logstash-5.5.0/conf/filebeat.conf
input {
  beats {
    port => 5044
        type => "logs"
        ssl => true
        ssl_certificate => "/etc/pki/tls/certs/logstash.crt"
        ssl_key => "/etc/pki/tls/private/logstash.key"
  }
}
output {
  elasticsearch { 
    hosts => ["127.0.0.1:9200"]
    user => elastic
    password => changeme
  }
  stdout { codec => rubydebug }
}
```

**防火墙设置**

```bash
firewall-cmd --permanent --add-port=5044/tcp
firewall-cmd --reload
```

**启动**

```bash
nohup bin/logstash -f conf/ &
```

## X-Pack

**离线安装 X-Pack**

```bash
cd /opt/
wget https://artifacts.elastic.co/downloads/packs/x-pack/x-pack-5.5.0.zip

/usr/local/elasticsearch-5.5.0/bin/elasticsearch-plugin install file:///opt/x-pack-5.5.0.zip
/usr/local/kibana-5.5.0-linux-x86_64/bin/kibana-plugin install file:///opt/x-pack-5.5.0.zip
/usr/local/logstash-5.5.0/bin/logstash-plugin install file:///opt/x-pack-5.5.0.zip
```

**参考**

- [Install X-Pack](https://www.elastic.co/guide/en/x-pack/current/installing-xpack.html)

## filebeat

**安装**

```bash
wget https://artifacts.elastic.co/downloads/beats/filebeat/filebeat-5.5.0-linux-x86_64.tar.gz
tar -xvzf filebeat-5.5.0-linux-x86_64.tar.gz
mv filebeat-5.5.0-linux-x86_64 /usr/local/
```

**配置 filebeat.yml**

```yaml
# vim /usr/local/filebeat-5.5.0-linux-x86_64/filebeat.yml
filebeat:
  prospectors:
    -
      paths:
        - /var/log/*
      input_type: log
      document_type: log
  registry_file: /var/lib/filebeat/registry

output:
  logstash:
    hosts: ["服务端IP:5044"]
    tls:
      certificate_authorities: ["/etc/pki/tls/certs/logstash.crt"]
```

**启动**

```bash
nohup ./filebeat -e -c filebeat.yml &
```

## 其他

**默认登录账户**

- elasticsearch: elastic/changeme
- kibana: elastic/changeme

**端口开通**

```bash
firewall-cmd --permanent --add-port=5601/tcp
firewall-cmd --reload
```

## 问题

> `max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]`

```bash
su root
vim /etc/sysctl.conf 
# 添加如下片段
# vm.max_map_count=655360
sysctl -p
```

> `max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]`

```bash
su root
vim /etc/security/limits.conf
# 添加以下片段
# * soft nofile 65536
# * hard nofile 131072
# * soft nproc 2048
# * hard nproc 4096
```

## 参考

- [ELK + filebeat 日志分析工具的部署和简单应用](http://www.jianshu.com/p/f6c7c8f1bce0)
- [搭建日志管理系统](https://beyondalbert.com/fan-yi-wen-da-jian-ri-zhi-guan-li-xi-tong/)
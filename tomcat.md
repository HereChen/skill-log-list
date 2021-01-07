# Tomcat

> <https://tomcat.apache.org>

## 安装

```bash
wget http://ftp.meisei-u.ac.jp/mirror/apache/dist/tomcat/tomcat-9/v9.0.26/bin/apache-tomcat-9.0.26.tar.gz -P /tmp
sudo tar xf /tmp/apache-tomcat-9*.tar.gz -C /opt/tomcat
```

## Commands

```bash
# cd tomcat_root_folder
# start
./bin/catalina start
./bin/startup.sh

# stop
./bin/catalina stop
./bin/shutdown.sh
```

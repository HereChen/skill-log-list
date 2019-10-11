# OpenCms

> <https://github.com/alkacon/opencms-core>

## 安装

1. java-1.8.0-openjdk
2. apache-tomcat-8.5.46
3. mariadb (安装最新的版本)，或者安装 mysql。
4. opencms-11.0.1

### CentOS OpenCms 环境配置

> CentOS-7-x86_64-DVD-1810.iso

```bash
# 环境配置中用到以下工具
sudo yum install vim wget unzip -y
```

**java**

```bash
# install
sudo yum install java-1.8.0-openjdk

# 查看 java 的安装目录
ls -lrt /usr/bin/java
ls -lrt /etc/alternatives/java

# 配置 java 环境变量
sudo vim ~/.bash_profile
# export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.222.b10-1.el7_7.x86_64/jre

source ~/.bash_profile
```

**tomcat**

```bash
# install
cd ~
wget https://www-us.apache.org/dist/tomcat/tomcat-8/v8.5.46/bin/apache-tomcat-8.5.46.tar.gz
mkdir /opt/tomcat
sudo tar xf ~/apache-tomcat-8*.tar.gz -C /opt/tomcat

# 配置 tomcat 启动参数
cd /opt/tomcat/apache-tomcat-8.5.46
sudo vim bin/catalina.sh
# JAVA_OPTS="-Djava.awt.headless=true"

# 配置 tomcat 环境变量
sudo vim ~/.bash_profile
# export CATALINA_HOME=/opt/tomcat/apache-tomcat-8.5.46

source ~/.bash_profile
```

**mysql**

```bash
# mariadb
sudo yum -y install mariadb-server mariadb

# 配置
sudo vim /etc/my.cnf
# [mysqld]
# max_allowed_packet=128M

# 启动并设置开机启动
sudo systemctl start mariadb
sudo systemctl enable mariadb
sudo systemctl status mariadb

# 设置数据库密码
sudo mysql_secure_installation
# 第一次执行，第一个选项回车键，第二个选项选择设置密码
```

**防火墙端口开放** tomcat 端口 8080，数据库端口 3306（用于允许外网连接，可选）。

```bash
sudo yum install firewalld firewall-config -y

sudo systemctl start firewalld.service
sudo systemctl enable firewalld.service
sudo systemctl status firewalld.service

# 开放 8080 和 3306 端口
firewall-cmd --permanent --add-port={8080/tcp,3306/tcp}
firewall-cmd --reload
```

### OpenCms 部署

**OpenCms** 部署和配置。

```bash
cd ~
wget http://www.opencms.org/downloads/opencms/opencms-11.0.1.zip
unzip -j opencms-11.0.1.zip opencms.war -d $CATALINA_HOME/webapps

cd $CATALINA_HOME
./bin/startup.sh
```

### OpenCms 配置

主要是配置数据库，浏览器进入 <http://192.168.100.137:8080/opencms/setup/>（更换 IP）开始配置。删除 Tomcat 部署的文件后，需要重新配置。

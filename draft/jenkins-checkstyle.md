# jenkins checkstyle

## CentOS 安装

```bash
# java
sudo yum install java

# jenkins
sudo wget -O /etc/yum.repos.d/jenkins.repo https://pkg.jenkins.io/redhat-stable/jenkins.repo
sudo rpm --import https://pkg.jenkins.io/redhat-stable/jenkins.io.key
sudo yum install jenkins

# 启动(start/stop)
sudo service jenkins start

# 访问: http://192.168.100.230:7000/
```

配置注意事项：

```bash
# 端口号更改此文件
vim /etc/sysconfig/jenkins

# 手动安装的 jdk 需要在此处添加 jdk 路径
# /usr/local/jdk1.8.0_131/bin/java
vim /etc/init.d/Jenkins
```

更改端口号后防火墙需要开放端口

```bash
# 安装
yum install firewalld firewall-config
# 启动防火墙
systemctl start firewalld.service
systemctl enable firewalld.service
systemctl status firewalld.service

# 添加端口
firewall-cmd --zone=public --permanent --add-port=7000/tcp
# 重启防火墙
firewall-cmd --reload

# 其他命令
firewall-cmd --state
firewall-cmd --list-all
# 查看端口列表
firewall-cmd --permanent --list-port
# 移除端口
firewall-cmd --zone=public --permanent --remove-port=7000/tcp
```

## Linux 手动安装

```bash
# jdk (目前需要 jdk1.8)
sudo wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/10.0.1+10/fb4372174a714e6b8c52526dc134031e/jdk-10.0.1_linux-x64_bin.tar.gz
tar zxvf jdk-10.0.1_linux-x64_bin.tar.gz

sudo vim ~/.bash_profile
# export JAVA_HOME=/usr/local/jdk-10.0.1
# export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH
source ~/.bash_profile

# jenkins
# yum -y install wget
# wget https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/latest/jenkins.war
curl -o jenkins.war https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/latest/jenkins.war

# 启动
nohup java -jar jenkins.war --httpPort=7000 &
```

## 命令

```bash
# 启动
net start jenkins

# 停止
net stop jenkins
```

## nginx 配置（可选）

```bash
# 安装
yum install epel-release
yum install nginx

# 配置 nginx
vim /etc/nginx/nginx.conf
# location /jenkins/ {
#   proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
#   proxy_set_header Host $http_host;
#   proxy_pass http://127.0.0.1:7000/;
# }

# 添加防火墙端口
firewall-cmd --zone=public --permanent --add-port=80/tcp
firewall-cmd --reload

# 启动 nginx 服务
sudo systemctl start nginx.service
# 开机启动
sudo systemctl enable nginx.service
# 重启 (或 service nginx restart)
systemctl restart nginx.service
```

如果报错，用以下方法解决：`[crit] 5472#0: *1 connect() to 127.0.0.1:7000 failed (13: Permission denied) while connecting to upstream,`

```bash
setsebool -P httpd_can_network_connect 1
```

## checkstyle

### 配置进入

1. http//IP:7000 进入
2. Gitlab Authentication plugin 插件安装: Manage Jenkins > Manage Plugins > Avaliable > Gitlab Authentication plugin 
3. SSH 配置: Credentials > ... > Private Key, Enter directly 添加服务器上 ssh-keygen 生成的 private key.
4. 新建 job: 配置 git repo、对应 Credentials、执行的任务.

### 任务配置

- 配置 git repo 和分支
- 配置任务执行触发条件.
- 配置执行的命令.
- 配置任务执行完成后操作: Checkstyle(`**/target/checkstyle-result.xml`), Findbugs(`**/target/findbugsXml.xml`)

### 前端任务配置

缺乏配置, 执行 npm gulp 等命令会提示 `npm command not found`.

- 安装 Nodejs Plugin
- jenkins 服务器上安装 nodejs
- Manage Jenkins > Global Tool Configuration > Add NodeJS > 取消 Install automatically 勾选 > 填写服务器 nodejs 安装目录.
- 任务配置中`Build Environment`勾选`Provide Node & npm bin/ folder to PATH`, 并在`NodeJS Installation`处选择配置的 nodejs

### 插件

1. Gitlab Authentication plugin
2. Checkstyle Plugin
3. FindBugs Plugin
4. Nodejs Plugin

## 重启

从浏览器中重启：`http://IP:7000/restart`

todo:
BOSS job, java 代码检查, 前端代码检查.

## 参考

1. [Jenkins Gitlab持续集成打包平台搭建](http://skyseraph.com/2016/07/18/Tools/Jenkins%20Gitlab%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%E6%89%93%E5%8C%85%E5%B9%B3%E5%8F%B0%E6%90%AD%E5%BB%BA/)
2. [Centos7（Firewall）防火墙开启常见端口命令](https://www.5yun.org/10074.html)

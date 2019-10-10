# mysql

```bash
# TODO: mariadb
yum -y install mariadb-server mariadb
sudo systemctl start mysqld
service mariadb start

# 初始化(设置密码)
sudo mysql_secure_installation

# 开放 3306 端口
# 参考 draft/elk.md
firewall-cmd --zone=public --add-port=3306/tcp --permanent
firewall-cmd --reload

# 通过 IP 连接
GRANT ALL PRIVILEGES ON *.* TO 'root'@'%' IDENTIFIED BY 'PASSWORD' WITH GRANT OPTION;
FLUSH PRIVILEGES;
```

## 安装(Windows)

1. 下载: <https://dev.mysql.com/downloads/mysql/>
2. 安装: <http://blog.csdn.net/darling_for/article/details/79070353>

    ```ini
    # 配置文件: D:\mysql-5.7.21-winx64/my.ini
    [mysql]
    default-character-set=utf8
    [mysqld]
    port = 3306
    basedir=D:\mysql-5.7.21-winx64
    datadir=D:\mysql-5.7.21-winx64\data
    max_connections=200
    character-set-server=utf8
    explicit_defaults_for_timestamp=true
    skip-grant-tables
    default-storage-engine=INNODB
    ```

    ```bash
    # 初始化, 会生成初始密码
    mysqld --initialize --user=mysql --console

    # 服务安装
    mysqld --install MySQL5.7.21

    # 服务启动
    net start MySQL5.7.21

    # 登录
    mysql -uroot -p密码

    # 密码变更
    set password for root@localhost=password('123456');

    # 停止服务
    net stop MySQL5.7.21
    # 刷新表
    flush privileges
    ```

## 安装(Linux)

```bash
# 各种问题....
# https://dev.mysql.com/doc/refman/8.0/en/binary-installation.html
cd /opt
wget https://cdn.mysql.com//Downloads/MySQL-8.0/mysql-8.0.12-linux-glibc2.12-x86_64.tar.xz

# Create a mysql User and Group
groupadd mysql
useradd -r -g mysql -s /bin/false mysql

# Obtain and Unpack the Distribution
cd /usr/local
tar xvf /opt/mysql-8.0.12-linux-glibc2.12-x86_64.tar.xz
ln -s mysql-8.0.12-linux-glibc2.12-x86_64 mysql

# add path
vim ~/.bashrc
# export PATH=$PATH:/usr/local/mysql/bin

cd mysql
mkdir mysql-files
chown mysql:mysql mysql-files
chmod 750 mysql-files

# log
mkdir /var/log/mariadb
chown -R mysql:mysql /var/log/mariadb/
mkdir /var/run/mariadb
chown -R mysql:mysql /var/run/mariadb/

ln -s /var/lib/mysql/mysql.sock /tmp/mysql.sock

# 配置文件位置
# /etc/my.cnf

# 初始化
mysqld --initialize --user=mysql --basedir=/usr/local/mysql --datadir=/usr/local/mysql/data

mysql_ssl_rsa_setup

# 启动
mysqld_safe --user=mysql &
```

## 安装(yum)

```bash
# 各种问题
# 安装说明 https://dev.mysql.com/doc/mysql-yum-repo-quick-guide/en/
# 下载 https://dev.mysql.com/downloads/repo/yum/
cd /opt
wget https://repo.mysql.com//mysql80-community-release-el7-1.noarch.rpm
rpm -Uvh mysql80-community-release-el7-1.noarch.rpm
yum install mysql-community-server

# 启动
service mysqld start

# 查看运行状态
service mysqld status

# 开机启动
systemctl enable mysqld
systemctl daemon-reload

# other
chown -R mysql:mysql /var/lib/mysql

# 用户组切换
newgrp mysql
```

## 安装(docker)

```bash
# simple
docker pull mysql:latest

docker run --name mysql -e MYSQL_ROOT_PASSWORD=123456 -p 3306:3306 -d mysql:latest

# 测试是否安装成功
docker exec -it 2d79a3cd70ff /bin/bash
mysql -hlocalhost -p3306 -uroot -p

# TODO: 客户端链接
# ALTER user 'root'@'%' IDENTIFIED WITH mysql_native_password BY '123456';
# FLUSH PRIVILEGES;
```

## 安装(macOS)

[download](https://dev.mysql.com/downloads/mysql/)

1. 8.x 下载 DMG 文件，安装后设置密码并立即启动服务，都是界面化操作。安装好后设置软连接即可使用。
2. 建立软连接

    ```bash
    sudo ln -s /usr/local/mysql/bin/mysql /usr/local/bin/mysql
    ```

3. GUI 工具[sequelpro](https://sequelpro.com), VSCode 可用 [vscode-mysql](https://github.com/formulahendry/vscode-mysql).

## command

```bash
# IP 登录
mysql -uroot -p -h192.168.100.137
```

```sql
-- 列出所有数据库
show databases;

-- 列出表格
show tables;

-- 创建数据库
CREATE DATABASE doc;
```

## Tips

1. 远程数据库复制到本地, 密码复杂的用双引号括起来(否则会报错).

    ```bash
    # [MySQL:将远程服务器的数据库拷到本地/复制他人数据库](http://blog.csdn.net/ycisacat/article/details/52587529)
    mysqldump -h '114.212.111.123' -uTHATUSER -pTHATPWD --opt --compress THATDB --skip-lock-tables | mysql -h localhost -uMYUSER -pMYPWD MYDB`
    ```

2. 备份数据库

    ```bash
    # mysqldump -hIP -PPORT -uUSERNAME -pPASSWORD 数据库名 > 数据库名.sql;
    mysqldump -h114.212.111.123 -P3306 -uroot -p8888 doc > doc.sql;
    ```

# MongoDB

> <https://www.mongodb.com>

## 命令

```bash
# install
wget https://fastdl.mongodb.org/linux/mongodb-linux-x86_64-4.0.2.tgz
tar -xvzf mongodb-linux-x86_64-4.0.2.tgz

# start
nohup mongod --dbpath=/home/mongodb_data &

mongod

# 查看数据库
show dbs

# 查看当前数据库
db

# 切换/创建数据库(不存在则创建)
use test_db

# 配置用户
use test
db.addUser('user','123456');

# 链接数据库
mongo 168.11.125.149:27017/test
```

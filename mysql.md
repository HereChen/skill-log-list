# mysql

1. 下载: <https://dev.mysql.com/downloads/mysql/>
1. 安装: <http://blog.csdn.net/darling_for/article/details/79070353>

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
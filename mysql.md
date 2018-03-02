# mysql

1. 下载: <https://dev.mysql.com/downloads/mysql/>
2. 安装: <http://blog.csdn.net/darling_for/article/details/79070353>

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

3. 远程数据库复制到本地, 密码复杂的用双引号括起来(否则会报错).

    ```bash
    # [MySQL:将远程服务器的数据库拷到本地/复制他人数据库](http://blog.csdn.net/ycisacat/article/details/52587529)
    mysqldump -h '114.212.111.123' -uTHATUSER -pTHATPWD --opt --compress THATDB --skip-lock-tables | mysql -h localhost -uMYUSER -pMYPWD MYDB`
    ```
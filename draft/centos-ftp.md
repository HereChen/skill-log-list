# ftp

<https://lnmput.github.io/2016/07/25/centos%E4%B8%8Bftp%E7%9B%B8%E5%85%B3%E8%AE%BE%E7%BD%AE/>

```bash
# 关闭防火墙
systemctl stop firewalld
systemctl disable firewalld

# 以上配置完成只能看到空文件夹, 看不到文件
# 将 SELINUX=enforcing 改为 SELINUX=disabled
vim /etc/selinux/config
reboot

# 安装
yum install vsftpd

# 配置
# 默认配置即可, 默认 ftp 根目录为 /var/ftp/
# vim /etc/vsftpd/vsftpd.conf

# 启动(CentOS 7)
systemctl restart vsftpd

# 启动时自动运行
systemctl enable vsftpd
```
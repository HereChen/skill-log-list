# Linux

- 压缩: `zip -r myzip.zip ./*`
- 解压: `unzip myzip.zip -d myzip`
- 压缩: `tar -czvf xxx.tar.gz folder`
- 解压缩: `tar -xzvf xxx.tar.gz`
- 复制当前文件夹下所有文件: `cp -r * ../folder`
- 复制文件内内容: `xclip -sel c < file`
- 进程查找: `ps aux | grep tomcat`

## Bash On Ubuntu On Windows 升级

- 查看当前版本(Bash): `lsb_release -a`
- 卸载(CMD): `lxrun /uninstall`
- 安装(CMD): `lxrun /install`
- 升级(Bash): `sudo do-release-upgrade`
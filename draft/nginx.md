# nginx

## 安装

### CentOS 在线安装

```bash
yum install epel-release
yum install nginx
systemctl start nginx
systemctl stop nginx
```

### 问题

> `while connecting to upstream Permission denied`

```bash
setsebool -P httpd_can_network_connect 1
```

## 常用命令

- 启动, `nginx.exe`
- 重启, `nginx.exe -s reload`

## 作为 Windows Service 自动启动

- [winsw](https://github.com/kohsuke/winsw)
- 复制 winsw-2.1.0-bin.exe 到 nginx 安装目录
- 新建同名文件 winsw-2.1.0-bin.xml

```xml
<service>
  <id>nginx</id>
  <name>nginx</name>
  <description>nginx</description>
  <executable>D:\nginx-1.13.1\nginx.exe</executable>
  <logpath>D:\nginx-1.13.1\</logpath>
  <logmode>roll</logmode>
  <depend></depend>
  <startargument>-p</startargument>
  <startargument>D:\nginx-1.13.1</startargument>
  <stopexecutable>D:\nginx-1.13.1\nginx.exe</stopexecutable>
  <stopargument>-p</stopargument>
  <stopargument>D:\nginx-1.13.1</stopargument>
  <stopargument>-s</stopargument>
  <stopargument>stop</stopargument>
</service>
```

- 安装 `winsw-2.1.0-bin.exe install`
- 卸载 `winsw-2.1.0-bin.exe uninstall`
- 停止 `winsw-2.1.0-bin.exe stop`
- `services.msc` 打开找到 nginx 服务项, 右键 start

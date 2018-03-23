## Fiddler

- 使用 Fiddler 时关闭代理 (比如：Shadowsocks)
- 开启流模式：点击工具栏 Stream
- 禁止缓存：Rules -> Performance -> Disable Caching
- 资源大小占比饼状图：Statistics -> Show Chart
- 隐藏图片请求：Rules -> Hide Image Requests

- Timeline 颜色 <https://imququ.com/post/timeline-in-fiddler.html>
    - 浅绿色 图片
    - 绿色 javascript
    - 紫色 css
    - 请求中的黑色竖线，表示的是浏览器收到服务端响应的第一个字节这一时刻。这个时间受 DNS 解析、建立连接、发送请求、等待服务端响应等步骤的影响。


## 手机APP抓包

条件: 手机和PC链接同一个局域网(同一个 Wifi).

1.允许 Fiddler 程序通过防火墙(Windows: 控制面板->防火墙->允许程序...).
2.Fiddler tools -> options -> HTTPS 和 Connections 下设置允许, Connections 下端口设置为 8888.
3.手机配置所连接的 Wifi 的 HTTP 代理为手动, IP 设置为 PC 的 IP, 端口设置为 8888.
4. 手机端进入浏览器, 进入 `http://IP:8888`, 安装证书.

备注:

1. iOS 10.3 设置: 通用 -> 关于本机 -> 证书信任设置.
2. Fiddler 可以设置过滤, 只看需要关注的客户端的请求.
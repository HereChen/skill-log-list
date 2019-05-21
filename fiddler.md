# Fiddler

* 使用 Fiddler 时关闭代理 (比如：Shadowsocks)
* 开启流模式：点击工具栏 Stream
* 禁止缓存：Rules -> Performance -> Disable Caching
* 资源大小占比饼状图：Statistics -> Show Chart
* 隐藏图片请求：Rules -> Hide Image Requests
* Timeline 颜色 <https://imququ.com/post/timeline-in-fiddler.html>
    1. 浅绿色 图片
    2. 绿色 javascript
    3. 紫色 css
    4. 请求中的黑色竖线，表示的是浏览器收到服务端响应的第一个字节这一时刻。这个时间受 DNS 解析、建立连接、发送请求、等待服务端响应等步骤的影响。
* 查看 gzip 内容：inspectors > 点击响应部分 Raw > 上面的显示的 `Response body is encoded. Click to decode`

## 手机APP抓包

条件: 手机和PC链接同一个局域网(同一个 Wifi).

1. [Windows] 允许 Fiddler 程序通过防火墙(Windows: 控制面板->防火墙->允许程序...).
2. [Fiddler-HTTPS] Fiddler tools -> options -> HTTPS(Decrypt HTTPS traffic).
3. [Fiddler-允许远程访问] Fiddler tools -> options -> Connections(Allow remote computers to connect) 下设置允许, Connections 下端口设置为 8888.
4. [手机-Wifi代理] 手机配置所连接的 Wifi 的 HTTP 代理为手动, IP 设置为 PC 的 IP, 端口设置为 8888.
5. [手机-证书] 手机端进入浏览器, 进入 `http://IP:8888`, 安装证书.

如果是 PC, 没有无线网卡的情况, 有两种方法解决:

1. PC 主机加一个无线网卡, 比如 USB Wifi.
2. 手机 USB 连接 PC 主机, 手机上设置 USB 共享网络. 比如(Android): 设置 -> 网络共享与便携式热点 -> USB绑定.

备注:

1. iOS 10.3 设置: 通用 -> 关于本机 -> 证书信任设置.
2. Fiddler 可以设置过滤, 只看需要关注的客户端的请求.

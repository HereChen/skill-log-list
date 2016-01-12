## Fiddler

- 开启流模式：点击工具栏 Stream
- 禁止缓存：Rules -> Performance -> Disable Caching
- 资源大小占比饼状图：Statistics -> Show Chart

- Timeline 颜色 <https://imququ.com/post/timeline-in-fiddler.html>
    - 浅绿色 图片
    - 绿色 javascript
    - 紫色 css
    - 请求中的黑色竖线，表示的是浏览器收到服务端响应的第一个字节这一时刻。这个时间受 DNS 解析、建立连接、发送请求、等待服务端响应等步骤的影响。
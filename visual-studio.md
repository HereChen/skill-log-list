# Visual Studio

- Visual Studio Shift + Alt 上下 多行选择
- Visual Studio 禁止 CSS 自动刷新加载

    <appSettings>
      <!--禁止自动刷新加载 CSS-->
      <add key="vs:EnableBrowserLink" value="false"/>
    </appSettings>

- 设置网站端口
    1. 网站 Project 右键属性
    2. Web -> Servers -> Project Url

使用场景：新建两个网站项目，一个网站调用另外一个网站的 API，此时固定端口可以方便的调用接口。

reference: <http://stackoverflow.com/questions/21202885/how-can-i-change-iis-express-port-for-a-site>
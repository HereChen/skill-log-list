# .NET

## .NET Core

### quick start

下载地址：<https://dotnet.microsoft.com/download>

```bash
# https://dotnet.microsoft.com/learn
# web app
dotnet new webApp -o myWebApp --no-https
cd myWebApp
dotnet run

# console app
dotnet new console -o myApp
cd myApp
dotnet run

# web api
dotnet new webapi -o TodoApi
cd TodoApi
dotnet run
# https://localhost:5001/WeatherForecast 访问接口
```

### Ubuntu 安装

```bash
# https://dotnet.microsoft.com/download/dotnet-core/3.0

# Ubuntu
# https://dotnet.microsoft.com/download/linux-package-manager/ubuntu19-04/sdk-3.0.100
sudo wget -q https://packages.microsoft.com/config/ubuntu/19.04/packages-microsoft-prod.deb -O packages-microsoft-prod.deb
sudo dpkg -i packages-microsoft-prod.deb
sudo apt update
sudo apt install apt-transport-https
sudo apt install dotnet-sdk-3.0
dotnet --version
```

### 实时编译 Web App

> [Razor file compilation in ASP.NET Core](https://docs.microsoft.com/en-us/aspnet/core/mvc/views/view-compilation?view=aspnetcore-3.0)

AspNet 变更页面内容后，在浏览器中刷新内容不会更新，需要增加以下依赖。

1. 增加依赖

    ```bash
    dotnet add package Microsoft.AspNetCore.Mvc.Razor.RuntimeCompilation --version 3.0.0
    ```

2. `Startup.cs` 增加一行

    ```diff
    public void ConfigureServices(IServiceCollection services)
    {
      services.AddRazorPages();
    +  services.AddControllersWithViews().AddRazorRuntimeCompilation();
    }
    ```

## CSharp

### 利用基类方法传递参数

```csharp
public void function(Type var1, Type var2, Typ2 var3)
  : base(var1, var2)
{
  // sentence here
}
```

### virtual

virtual 关键字用于指定属性或方法时可以在派生类中重写。

### abstract

抽象类用做基类，不能被实例化，用途是派生出其他非抽象类。

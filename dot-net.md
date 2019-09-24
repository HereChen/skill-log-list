# .NET Core

## 安装

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

## C#

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

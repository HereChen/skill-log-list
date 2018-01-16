# React Native

<!-- toc -->

> 1. [React Native 主页](https://facebook.github.io/react-native)
> 2. 示例项目: [amazing-react-projects](https://github.com/jiwonbest/amazing-react-projects)

示例项目 python 和 node-gyp-bin 相关错误可以尝试先执行 `yar add node-sass` 或者 `npm install -f node-sass` (<https://github.com/sass/node-sass/issues/1980>).
## 环境配置

> https://facebook.github.io/react-native/docs/getting-started.html

### 系统环境

1. 安装 [nodejs](https://nodejs.org).
2. `npm install -g react-native-cli`.

**Android**

1. JDK (并配置环境变量)
2. 安装 Android Studio <http://www.android-studio.org>
3. 通过 SDK Manager 下载 SDK, 并配置环境变量.

```
# 新建环境变量
ANDROID_HOME, C:\Users\chenl\AppData\Local\Android\Sdk
# 添加路径到 path
%ANDROID_HOME%\tools
%ANDROID_HOME%\platform-tools
```

**IOS**

需要安装 XCode.

### 编辑器

**Visual Studio Code**

安装扩展 `React Native Tools` 用于调试.

**Atom**

> https://atom.io/packages/nuclide

## Android

**Demo**

```bash
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
```

**other**

1. 选择物理设备 `adb devices`, 查看当前的 Android 设备.
2. `Ctrl + M` 打开菜单 (Android Studio自带虚拟机没有菜单和摇晃手机, 可以这种方式打开菜单).

### 打包

> 1. https://facebook.github.io/react-native/docs/signed-apk-android.html
> 2. https://reactnative.cn/docs/0.51/signed-apk-android.html
> 3. https://www.jianshu.com/p/1380d4c8b596

**1. 生成签名密钥**

```bash
$ keytool -genkey -v -keystore my-release-key.keystore -alias my-key-alias -keyalg RSA -keysize 2048 -validity 10000
Enter keystore password:
Keystore password is too short - must be at least 6 characters
Enter keystore password: chenlei
Re-enter new password: chenlei
What is your first and last name?
  [Unknown]:  HereChen
What is the name of your organizational unit?
  [Unknown]:  HereChen
What is the name of your organization?
  [Unknown]:  HereChen
What is the name of your City or Locality?
  [Unknown]:  Chengdu
What is the name of your State or Province?
  [Unknown]:  Sichuan
What is the two-letter country code for this unit?
  [Unknown]:  51
Is CN=HereChen, OU=HereChen, O=HereChen, L=Chengdu, ST=Sichuan, C=51 correct?
  [no]:  yes

Generating 2,048 bit RSA key pair and self-signed certificate (SHA256withRSA) with a validity of 10,000 days
        for: CN=HereChen, OU=HereChen, O=HereChen, L=Chengdu, ST=Sichuan, C=51
Enter key password for <my-key-alias>
        (RETURN if same as keystore password):
[Storing my-release-key.keystore]
```

**2. gradle设置**

1. `my-release-key.keystore` 文件放到工程 `android/app` 文件夹下.
2. 编辑 `android/app/gradle.properties`, 添加如下信息.

```
MYAPP_RELEASE_STORE_FILE=my-release-key.keystore
MYAPP_RELEASE_KEY_ALIAS=my-key-alias
MYAPP_RELEASE_STORE_PASSWORD=chenlei
MYAPP_RELEASE_KEY_PASSWORD=chenlei
```

3. 编辑 `android/app/build.gradle`, 添加如下信息.

```
...
android {
    ...
    defaultConfig { ... }
    signingConfigs {
        release {
            storeFile file(MYAPP_RELEASE_STORE_FILE)
            storePassword MYAPP_RELEASE_STORE_PASSWORD
            keyAlias MYAPP_RELEASE_KEY_ALIAS
            keyPassword MYAPP_RELEASE_KEY_PASSWORD
        }
    }
    buildTypes {
        release {
            ...
            signingConfig signingConfigs.release
        }
    }
}
...
```

**3. 打包**

```bash
cd android && ./gradlew assembleRelease
```

打包后在 `android/app/build/outputs/apk/app-release.apk`. 

**安装方式**

1. Genymotion 可以拖拽 apk 进行安装.
2. `adb install app-release.apk` 安装.

如果报签名错误, 可先卸载之前的 debug 版本.

### 其他

**入口文件更改**

> 从0.49开始, 只有一个入口, 不区分 ios 和 android. <https://github.com/facebook/react-native/releases/tag/v0.49.0>

React Native CLI 新建的工程, 默认入口是 `index.js`. 在 `android\app\build.gradle` 中更改入口.

```javascript
project.ext.react = [
    entryFile: "index.android.js"
]
```

对应更改 `android\app\src\main\java\com\**\MainApplication.java`.

```java
protected String getJSMainModuleName() {
  return "index.android";
}
```

## IOS

IOS 版本编译需要在 Mac 上进行.

```
brew install node
brew install watchman
npm install -g react-native-cli

react-native init AwesomeProject
cd AwesomeProject
react-native run-ios
```

## 工具/依赖(dependencies)

### 导航

> https://facebook.github.io/react-native/docs/navigation.html

1. [react-navigation](https://github.com/react-navigation/react-navigation) 提供了常用的导航方式(Stack, Tab, Drawer), 推荐.
2. [NavigatorIOS](https://facebook.github.io/react-native/docs/navigatorios.html) 为内建的导航, 仅在 IOS 上可用.

### UI

尚未找到两端(Web, Native)完整好用的 UI, 若后端采用 ant-design 可用 ant-design-mobile.

1. [ant-design-mobile](https://github.com/ant-design/ant-design-mobile) 每个组件是否支持 Native 有说明.
2. [react-native-elements](https://github.com/react-native-training/react-native-elements)
3. [NativeBase](https://github.com/GeekyAnts/NativeBase)

### HTTP 请求

> https://facebook.github.io/react-native/docs/network.html

1. [fetch](https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API) 为内建接口.
2. [**axios**](https://github.com/axios/axios) 为使用校广泛的第三方请求库, 推荐使用.

## 调试

> https://facebook.github.io/react-native/docs/debugging.html

根据提示, 可以菜单按钮选择重新加载或热加载. Android 可摇晃手机显示菜单.

### 虚拟机

1. [Genymotion](https://www.genymotion.com/download/), 需要先注册, 然后选择 for personal 使用. 如果系统开启了 Hyper-V, 需要先关闭.
2. Android Studio 内建虚拟机, 同样需要关闭 Hyper-V.
3. [Visual Studio Emulator for Android](https://www.visualstudio.com/vs/msft-android-emulator/) 需要开启 Hyper-V.

### 调试工具: Chrome

1. `Remote JS Debugging` 开启JS调试.
2. 浏览器端进去 `http://localhost:8081/debugger-ui/`, 并开启开发工具.
3. 可在 Sources 中设置断点或者代码中写入 `debugger`.

### 调试工具: VSCode

1. 安装扩展: React Native Tools.
2. F5 生成 launch.json 文件.
3. 进入调试菜单(Ctrl + Shift + D), 选择 Debug Android.
4. 设置断点或者写入 `debugger` 开始调试, 在 output 栏输出.

### HTTP 调试问题备注

应用 Fiddler 调试 HTTP, 模拟器设置了代理后, APP 无法热加载 JS bundle. 目前只有用 Chrome 或者断点的方式来调试.

## 工程结构

> 1. [Organizing a React Native Project](https://medium.com/the-react-native-log/organizing-a-react-native-project-9514dfadaa0)
> 2. [React native project setup — a better folder structure](https://hackernoon.com/manage-react-native-project-folder-structure-and-simplify-the-code-c98da77ef792)

```
android/         # Android 工程
ios/             # IOS 工程
src/             # 开发前端资源
  -- assets/     # 静态资源
  -- components/ # 组件
  -- api/        # 接口
  -- route/      # 导航(路由)
  -- config/     # 常量配置
  -- screens/    # 页面/功能
  -- utils/      # 常用工具
  -- reducers 相关
  -- index.js    # APP 入口
index.js         # 入口文件
```

## 问题及解决

1. VSCode Debug 无法加载的情况, 首先重启 VSCode 再启动项目.
2. 添加`antd-mobile`后报错, 无法解析 `react-dom`, 依赖中加入`react-dom`并安装即可.
3. 集成`react-native-navigation`需要注意Android SDK版本, 版本过低可能出现编译错误(`Error:Error retrieving parent for item: No resource found`).
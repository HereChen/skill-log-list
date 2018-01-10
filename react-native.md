# React Native

> 1. <https://facebook.github.io/react-native>
> 2. <https://facebook.github.io/react-native/docs/getting-started.html>
> 3. 示例项目: <https://github.com/jiwonbest/amazing-react-projects>

示例项目 python 和 node-gyp-bin 相关错误可以尝试先执行 `yar add node-sass` 或者 `npm install -f node-sass` (<https://github.com/sass/node-sass/issues/1980>).
## 环境配置

```bash
# install nodejs
npm install -g react-native-cli
```

**Atom**

> https://atom.io/packages/nuclide

## Android

### 环境及Demo

1. 安装 Android Studio <http://www.android-studio.org>
2. 虚拟机下载: <https://www.genymotion.com/download/>

```
# 新建环境变量
ANDROID_HOME, C:\Users\chenl\AppData\Local\Android\Sdk
# 添加路径到 path
%ANDROID_HOME%\tools
%ANDROID_HOME%\platform-tools
```

**Demo**

```bash
react-native init AwesomeProject
cd AwesomeProject
react-native run-android
```

**other**

1. 选择物理设备 `adb devices`, 查看当前的 Android 设备.
2. `Ctrl + M` 打开菜单 (Android Studio自带虚拟机没有菜单和摇晃手机, 可以这种方式打开菜单).

**问题**

1. Android Emulator(Genymotion 和 Android Studio 自带虚拟机) 与 Hyper-V 不兼容. 需要关闭 Hyper-V.

```bash
# turn off Hyper-V

# turn on Hyper-V
```

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

## 调试

> https://facebook.github.io/react-native/docs/debugging.html

根据提示, 可以菜单按钮选择重新加载或热加载. Android 可摇晃手机显示菜单.

### Chrome 调试

1. `Remote JS Debugging` 开启JS调试.
2. 浏览器端进去 `http://localhost:8081/debugger-ui/`, 并开启开发工具.
3. 可在 Sources 中设置断点或者代码中写入 `debugger`.

### VSCode 调试

1. 安装扩展: React Native Tools.
2. F5 生成 lunch.json 文件.
3. 进入调试菜单(Ctrl + Shift + D), 选择 Debug Android.
4. 设置断点或者写入 `debugger` 开始调试.

## 工程结构

> [Organizing a React Native Project](https://medium.com/the-react-native-log/organizing-a-react-native-project-9514dfadaa0)

```
android/
ios/
app/
 -- components/
 -- config/
 -- screens/
 -- actions/
 -- reducers/
 -- index.js
```

> [React native project setup — a better folder structure](https://hackernoon.com/manage-react-native-project-folder-structure-and-simplify-the-code-c98da77ef792)

```
android/
ios/
public/
src/
  --components/
  --scenes/
  --style/
  --utils/
  --constants.js
```

## Tips

1. 图片引用
2. style 书写: CSS 改成小驼峰.

## 问题及解决

1. VSCode Debug 无法加载的情况, 首先重启 VSCode 再启动项目.
2. 添加`antd-mobile`后报错, 无法解析 `react-dom`, 依赖中加入`react-dom`并安装即可.
3. 集成`react-native-navigation`需要注意Android SDK版本, 版本过低可能出现编译错误(`Error:Error retrieving parent for item: No resource found`).
# React Native

> 1. <https://facebook.github.io/react-native>
> 2. <https://facebook.github.io/react-native/docs/getting-started.html>
> 3. 示例项目: <https://github.com/jiwonbest/amazing-react-projects>

示例项目 python 和 node-gyp-bin 相关错误可以尝试先执行 `yar add node-sass` 或者 `npm install -f node-sass` (<https://github.com/sass/node-sass/issues/1980>).

## Android

1. 安装 Android Studio <http://www.android-studio.org>
2. 虚拟机下载: <https://www.genymotion.com/download/>

```
# 新建环境变量
ANDROID_HOME, C:\Users\chenl\AppData\Local\Android\Sdk
# 添加路径到 path
%ANDROID_HOME%\tools
%ANDROID_HOME%\platform-tools
```

2. `npm install -g react-native-cli`

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

> https://medium.com/the-react-native-log/organizing-a-react-native-project-9514dfadaa0

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
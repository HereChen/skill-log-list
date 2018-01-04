# React Native

> 1. <https://facebook.github.io/react-native>
> 2. <https://facebook.github.io/react-native/docs/getting-started.html>

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

重新加载: 摇晃手机选择重新加载.

**other**

```
1. 选择物理设备 `adb devices`, 查看当前的 Android 设备.
```

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
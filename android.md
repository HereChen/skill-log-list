# Android

## adb

> <http://adbshell.com/>

```bash
# 启动 adb 服务
adb start-server

# 关闭 adb 服务
adb kill-server
```

```bash
# wifi 情况下 adb 连接手机
# step 1: USB 连接手机
adb tcpip 5555

# step 2: adb wifi 连接手机
adb connect IP:5555

adb devices

# refer
# https://developer.android.google.cn/studio/command-line/adb
# http://adbshell.com/commands/adb-connect
```
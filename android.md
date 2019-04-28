# Android

## adb

> <http://adbshell.com/>

**重启 ADB**

```bash
# 启动 adb 服务
adb start-server

# 关闭 adb 服务
adb kill-server
```

**ADB Wifi 连接手机**

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

**抓取日志**

```bash
adb logcat
```

## Android Emulator DNS

```bash
# 场景: 台式机联网
# https://blog.csdn.net/weixin_42306122/article/details/82563925
# step 1: 启动模拟器

# step 2
adb root
adb shell
# getprop 查看配置, 根据需要配置
setprop net.dns1 8.8.8.8
setprop net.eth0.dns1 8.8.8.8
setprop net.eth0.gw 8.8.8.8

# step 3: 链接 AndroidWifi
```

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

**安装 APK**

```bash
# 安装到默认设备
adb install <PATH TO APK>

# 安装到指定设备
adb -s <DEVICE ID> install <PATH TO APK>
```

**端口映射** React Native 调试可用.

```bash
adb -s <DEVICE ID> reverse tcp:8081 tcp:8081
```

**自签名 HTTPS 证书服务访问**

1. Android 工程配置允许系统或用户安装的证书: `android\app\src\main\res\xml\network_security_config.xml`

    ```xml
    <network-security-config>
        <domain-config cleartextTrafficPermitted="true">
            <domain includeSubdomains="true">localtest.com</domain>

            <trust-anchors>
                <certificates src="system" />
                <certificates src="user" />
            </trust-anchors>
        </domain-config>
    </network-security-config>
    ```

2. Android 手机设备安装生成的 cert 证书. 可将证书文件拷贝到手机存储器上, 从存储器上选择安装.

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

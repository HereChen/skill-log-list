# Android

## adb

```bash
# wifi 情况下 adb 连接手机
# step 1: USB 连接手机
adb tcpip 5555

# step 2: adb wifi 连接手机
adb connect IP:5555

adb devices
```
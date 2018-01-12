# Weex

> http://weex.apache.org

问题: 入口在哪儿?

**案例**

1. [网易严选](https://github.com/zwwill/yanxuan-weex-demo)
2. [点我达骑手Weex最佳实践](https://mp.weixin.qq.com/s/dowOE_QpZrtV5GH9EAgyHg)
2. [weexteam/weex-hackernews](https://github.com/weexteam/weex-hackernews)

## 搭建开发环境

```
npm install -g weex-toolkit
```
## Demo

**web**

```
weex create weex
cd weex
npm install
npm run dev & npm run serve
```

**命令**

> https://github.com/weexteam/weex-pack

```bash
# debug
weex debug

# add platform
weex platform add android
weex platform add ios

# run
weex run web
weex run android
weex run ios

# build
weex build web
```

## 问题及解决

1. `https://maven.google.com/` 链接不上, 更改`\platforms\android\build.gradle`文件, 换成 `https://dl.google.com/dl/android/maven2/`。
2. `adb: failed to stat app/build/outputs/apk/playground.apk: No such file or directory`, 替换 `platforms/android/app/build.gradle` 文件中的 `weex-app.apk` 为 `playground.apk`.
3. `weex debug` 报错可先安装 `npm install -g weex-devtool`.
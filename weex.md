# Weex

> http://weex.apache.org

**案例**

1. [网易严选](https://github.com/zwwill/yanxuan-weex-demo)
2. [点我达骑手Weex最佳实践](https://mp.weixin.qq.com/s/dowOE_QpZrtV5GH9EAgyHg)

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

```
weex platform add android
weex platform add ios

weex run web
weex run android
weex run ios

weex build web
```

## 问题及解决

1. `https://maven.google.com/` 链接不上, 更改`\platforms\android\build.gradle`文件, 换成 `https://dl.google.com/dl/android/maven2/`。
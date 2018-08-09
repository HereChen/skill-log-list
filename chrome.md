# Chrome

- 各个功能项可以拖动改变顺序
- Ctrl + ]/[ 可以切换功能页
- 文本编辑, 地址栏输入 `data:text/html, <html contenteditable>`

## Settings

- Prefference > Console > Show timestamps: 勾选后 Console 中输出, 包含输出时间

## Elements

- 选中元素，按 h 键，可以切换显示隐藏状态

## Sources

- Ctrl + D 连续多选
- Ctrl + P 打开文件
- Ctrl + Shift + P 打开 CSS/JS 后，定位 CSS 选择器/JS 函数

## Network

- 蓝线: HTML加载解析完毕
- 红线: css、js、图片等资源下载完毕
- 紫线: 前两个事件同时发生
- 排除特定文件格式响应信息： 使用负号排除图片，filter 中输入 `-png -js` 可排除 png 和 js
- 清除 Application Cache： chrome://appcache-internals/

## Console

- Ctrl + L 清空 Console

## 离线安装扩展

进入扩展程序页面，打开开发者模式，macOS 上可以直接拖入 zip 包安装，Windows 上解压后，加载解压的扩展（加载已解压的扩展程序/Load unpacked）。crx 扩展的可以直接改后缀类似操作。可用 [octotree](https://github.com/buunguyen/octotree) 作为上手示例，提供了 zip 和 crx。

## 参考/资源

- [草依山, chrome开发者工具部分忽略的功能](http://jser.me/2015/08/25/chrome%E5%BC%80%E5%8F%91%E8%80%85%E5%B7%A5%E5%85%B7%E9%83%A8%E5%88%86%E5%BF%BD%E7%95%A5%E7%9A%84%E5%8A%9F%E8%83%BD.html)
- [Chrome 35个开发者工具的小技巧](http://www.w3cplus.com/tools/dev-tips.html)

# Chrome

## Chrome Network

- 蓝线: HTML加载解析完毕
- 红线: css、js、图片等资源下载完毕
- 紫线: 前两个事件同时发生
- 排除特定文件格式响应信息： 使用负号排除图片，filter 中输入 `-png -js` 可排除 png 和 js
- 清除 Application Cache： chrome://appcache-internals/
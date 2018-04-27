# Windows

- (截屏)将选择区域图像复制到剪贴板: `Win + Shift + S`
- 桌面切换: `Win + Ctrl + Left/Right`
- 显示日期: `Win + Alt + D`

## 开启休眠

1. powercfg.exe /hibernate on
2. 在电源设置里面勾选 hibernate ：Start -> System -> Power & sleep -> Additional power settings. -> Choose what the power button does -> Change settings that are currently unavailable -> 勾选Hibernate

## 命令

1. 查看端口占用进程: `netstat -ano | findstr "8081"`
2. 杀进程: `taskkill /pid XXXXXX`, 或者任务管理器关闭进程。
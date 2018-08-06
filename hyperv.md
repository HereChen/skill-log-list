# Hyper-V

TODO: 启用后开启和关闭 Hyper-V。

## Ubuntu 全屏设置

问题体现为，Ubuntu 分辨率设置显示为 `Unknow display`，不能更改分辨率。

```bash
sudo apt-get install linux-image-extra-virtual
sudo gedit /etc/default/grub
# 1920x1080 分辨率
GRUB_CMDLINE_LINUX_DEFAULT="quiet splash video=hyperv_fb:1920x1080"
sudo update-grub
# 重启系统
```

[How can I increase the Hyper-V display resolution?](https://superuser.com/questions/518484/how-can-i-increase-the-hyper-v-display-resolution)

## 小技巧

1. Windows 屏幕大小设置：设置分辨率即可更改屏幕大小。
2. 快速建立虚拟机：可直接复制现有的 vhdx 虚拟机硬盘文件，然后导入。

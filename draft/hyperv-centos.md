# Hyper-V + CentOS 7.3

<http://blog.csdn.net/chris_111x/article/details/52313797>

## 准备

1. Linux Integration Services, LinuxIC-4.1.3-2.iso, <https://www.microsoft.com/en-us/search/result.aspx?q=Linux+Integration+Services&Preview=1&search=>
2. CentOS-7-x86_64-Everything-1611.iso, <http://mirrors.163.com/centos/>

## 安装配置

## 网络配置

1. Hyper-V 配置, Virtual Switch Manager 配置 External 网络(注意选择正确的External Network), CentOS 虚拟机选择配置的网络.
2. Hyper-V, Media -> DVD Drive -> Insert Disk..., 选择 LinuxIC-4.1.3-2.iso
2. CentOS 配置

```bash
mount /dev/cdrom /media
cd /media
./install.sh
```

```bash
# ONBOOT=no 改成 ONBOOT=yes
vi /etc/sysconfig/network-scripts/ifcfg-eth0
# 重启网路
service network restart
# 查看 ip
ip address
```

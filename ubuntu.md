# Ubuntu

## 初始

1. 安装常用软件

    ```text
    # Chrome Dev 版本
    # Visual Studio Code
    # Intellij Idea
    # JDK
    sudo apt install ibus-pinyin
    sudo apt install maven
    sudo apt install git
    sudo apt install vim
    sudo apt install curl

    # lenovo-k20 ubuntu 18.04
    # sudo apt install intel-microcode
    ```

2. 添加中文输入法（先安装 `sudo apt install ibus-pinyin`，再添加中文语言，再添加输入法）。
3. 更改软件源为国内的。
4. 创建软连接，指向其他的硬盘。

## command

```bash
# update
sudo apt update
sudo apt upgrade

# deb 软件安装
sudo dpkg -i software-name.deb

# 软禁删除
sudo apt remove software-name

# command alias
alias ll='ls -la'

# root
sudo su -

# 设置 root 密码
sudo passwd root

# run program background
firefox &

# clear terminal
clear

# check var
echo $shell

# list every file
ls -la

# help
man ls

# list similar
ls myfile*

# create file
touch filename

# locating files
which perl
sudo / -name "*log*" -print

# create a var
export PATH=$PATH:~/bin

# zip
zip myfile.zip ./*
zip myfile.zip myfile

# tar: compression tar
tar cfzv mytar.tar.gz myfile

# tar: unpack
tar xfzv mytar.tar.gz

# tar: unpack to destination
tar xfzv mytar.tar.gz -C /folder/

# exploer open folder
nautilus /folder/
```

### sharing file

```bash
sudo vi /edc/samba/smb.conf
sudo service samba restart
```

## 系统升级

```bash
# https://medium.com/@rockey5520/wsl-ubuntu-upgrade-to-disco-dingo-19-04-b4abff20452d
sudo apt upgrade
sudo do-release-upgrade
# 此时提示修改 /etc/update-manager/release-upgrades Prompt = normal, 按照提示修改, 并再次执行
sudo do-release-upgrade
# 如果是 WSL, 安装完成后重启, 以管理员模式在 PowerShell 中执行 `Restart-Service LxssManager`
```

## 镜像替换

```bash
sudo vim /etc/apt/sources.list
# us.archive.ubuntu.com 替换为 mirrors.aliyun.com
# :%s/us\.archive\.ubuntu\.com/mirrors\.aliyun\.com/g
# security.ubuntu.com 替换为 mirrors.aliyun.com
# :%s/security\.ubuntu\.com/mirrors\.aliyun\.com/g

# http://mirrors.aliyun.com/ubuntu/
# http://mirrors.163.com/ubuntu/
# http://mirrors.sohu.com/ubuntu/
# http://mirrors.tuna.tsinghua.edu.cn
```

## 桌面版启用 SSH 登录

如果在虚拟机中安装 Ubuntu 桌面版，并且需要交换文件，启用 SSH 登录后，就可以通过 FileZilla 这类工具上传和下载文件，从而实现和虚拟机内的文件交换。

```bash
# 桌面版本有客户端，没有服务端
sudo apt install openssh-server
sudo apt install openssh-client
# 配置位置 /etc/ssh/sshd_config

sudo service ssh restart
```

## bash 终端添加 git 当前分支显示

> <https://askubuntu.com/a/946716>

```sh
# vim ~/.bashrc
# source ~/.bashrc

# Show git branch name
force_color_prompt=yes
color_prompt=yes
parse_git_branch() {
 git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}
if [ "$color_prompt" = yes ]; then
 PS1='${debian_chroot:+($debian_chroot)}\[\033[01;32m\]\u@\h\[\033[00m\]:\[\033[01;34m\]\w\[\033[01;31m\]$(parse_git_branch)\[\033[00m\]\$ '
else
 PS1='${debian_chroot:+($debian_chroot)}\u@\h:\w$(parse_git_branch)\$ '
fi
unset color_prompt force_color_prompt
```

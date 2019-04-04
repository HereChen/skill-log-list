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

# command alias
alias ll='ls -la'

# root
sudo su -

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

## 镜像替换

```bash
sudo vim /etc/apt/sources.list
# us.archive.ubuntu.com 替换为 mirrors.aliyun.com
# :%s/us\.archive\.ubuntu\.com/mirrors\.aliyun\.com/g

# http://mirrors.aliyun.com/ubuntu/
# http://mirrors.163.com/ubuntu/
# http://mirrors.sohu.com/ubuntu/
# http://mirrors.tuna.tsinghua.edu.cn
```

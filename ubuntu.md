# Ubuntu

## 初始

1. 添加中文输入法。
2. 更改软件源为国内的。
3. 创建软连接，指向其他的硬盘。
4. 安装常用软件

    ```text
    Chrome Dev 版本
    Visual Studio Code
    Intellij Idea
    JDK
    maven
    ```

## command

```bash
# 更新软件
sudo apt update
sudo apt upgrade

# command alias
alias ll='ls -la'

# root
sudo su -

# run program background
firefox &
```

- clc: `clear`
- help: `ls --help`
- help: `man ls` `info`
- check var.: `echo $shell`
- internet Apps: pidgin thunderbird
- list every file: `ls -a`,`ls -la`
- list similar: `ls myfile*`
- create file: `touch filename`
- file permissions: use `chmod`
- copy: `cp filename drectory`
- move: `mv filename drectory`
- create a var: `export PATH=$PATH:~/bin`
- locating files: `which perl`, `sudo / -name "*log*" -print`
- redirection: `ls > ls.txt`, `ls >> ls.ntxt`
- shart file: `cat .bashrc`
- edit file: `nano file`,`vi file`
- compression zip: `zip myfile.zip ./*`, `zip myfile.zip myfile`
- compression tar: `tar cfzv mytar.tar.gz myfile`
- uncompression: `tar xfzv mytar.tar.gz`

### sharing file:
- `sudo vi /edc/samba/smb.conf`
- `sudo service samba restart`

# Git 学习笔记

## 安装

### Ubuntu

安装最新版的 git[^ubuntuInstallLastVersionGit]。

```bash
sudo add-apt-repository ppa:git-core/ppa
sudo apt-get update
sudo apt-get install git
```

如果上面执行报错 `Errors were encountered while processing: runit git-daemon-run`, 尝试执行下面命令.

```bash
sudo apt-get purge runit
sudo apt-get purge git-all
sudo apt-get purge git
sudo apt-get autoremove
sudo apt update
sudo apt install git
```

[^ubuntuInstallLastVersionGit]: [Installing Latest version of git in ubuntu](http://stackoverflow.com/questions/19109542/installing-latest-version-of-git-in-ubuntu/19109661#19109661), [How to fix processing with runit and git-daemon-run [duplicate]](http://askubuntu.com/questions/765565/how-to-fix-processing-with-runit-and-git-daemon-run/772095#772095)

### CentOS 从源码安装

执行 `yum install git` 安装的版本比较老, 安装最新版可从源码安装[^centOSInstallLastVersionGit]。

```bash
# 依赖工具安装
yum install curl-devel expat-devel gettext-devel openssl-devel zlib-devel
yum install gcc perl-ExtUtils-MakeMaker

# git 源码下载
# https://www.kernel.org/pub/software/scm/git/
curl -o git-2.9.3.tar.xz https://www.kernel.org/pub/software/scm/git/git-2.9.3.tar.xz
tar -xvJf git-2.9.3.tar.xz

# 编译安装 git
cd git-2.9.3
make prefix=/usr/local all
sudo make prefix=/usr/local install
```

[^centOSInstallLastVersionGit]: [How to install latest version of git on CentOS 6.x/7.x](http://stackoverflow.com/questions/21820715/how-to-install-latest-version-of-git-on-centos-6-x-7-x)
, [起步 - 安装 Git](https://git-scm.com/book/zh/v1/%E8%B5%B7%E6%AD%A5-%E5%AE%89%E8%A3%85-Git)

## Git 基础

* 退出 `git log`：英文键盘下，按 Q 键。
* 仓库中文件的三种状态：已提交(committed)--本地仓库，已修改(modified)--暂存区域、已暂存(staged)--工作目录。
* 初始化。初始化后会在工作目录中生成 `.git` 目录 。

    ```bash
    git init
    ```

* 跟踪文件。把跟踪文件纳入版本控制。

    ```bash
    git add -A
    ```

* 提交更新。提交更改注释。

    ```bash
    git commit -m "changes for commit"
    ```

* 克隆。克隆仓库到本地。

    ```bash
    git clone git://github.com/schacon/grit.git
    ```

* 查看状态。查看当前文件状态。

    ```bash
    git status
    ```

* 上传。上传至服务器。

    ```bash
    git push -u master
    ```

* 更新查看。查看尚未更新的文件更新的部分。

    ```bash
    git diff
    ```

* 移除文件。将文件从已跟踪文件清单移除。

    ```bash
    git rm filename
    ```

* 重命名文件。

    ```bash
    git mv file_from file_to
    ````

* 查看提交历史。

    ```bash
    git log
    ```

* 查看 Git 设置。

    ```bash
    git config --list
    ```

* 启动图形化界面。

    ```bash
    gitk
    ```

* 重新提交(修改最后一次提交)。比如刚提交，但是又忘了将几个文件纳入跟踪，此时可用。

    ```bash
    git commit --amend
    ```

* 取消暂存。在 add 后执行此条，则提交时将不包含此文件的更新。

    ```bash
    git reset HEAD filename
    ```

* 取消修改。

    ```bash
    git checkout -- filename
    ```

* 忽略文件。将不加入版本控制的文件在 `.gitignore` 文件中列出。
* 新建分支: `git checkout -b hunan`
* 清空 git 目录: `git clean -d -x -f`, `-x` 会删除 ignore 的文件 <http://stackoverflow.com/questions/673407/how-do-i-clear-my-local-working-directory-in-git>
* 关闭 `warning: LF will be replaced by CRLF` 警告, `git config --global core.safecrlf false`
* 设置当前 Repo 的账户

    ```bash
    git config user.name "HereChen"
    git config user.email "chenlei.here@qq.com"
    ```

### 合并分支(develop 合并到 master)

pull -> merge -> 修改冲突

1. 切换到 master 分支: git checkout master
2. 合并 develop 到 master: git merge develop
3. 提交(git bash 中 Esc+Shift, wq 保存退出), git push 上传

### commit

1. 修改提交的信息: `git commit --amend`

## Tips

### 删除分支

```bash
# 删除远程分支
git push -d origin BRANCH_NAME

# 删除本地分支
git branch -d BRANCH_NAME
```

### commit 叠加到远程分支上

即把本地的 commit，放到 pull 下来最后一个 commit 后面。

```bash
git pull --rebase
```

### 修改历史 commit 信息

* 只修改最后一条: `git commit --amend`
* 修改多条(比如最后 3 条, 或倒数第 3 条)
  * `git rebase -i HEAD~3`, 然后把要修改.
  * 把需要修改的 commit 前面的 `pick` 改为 `reword`, 保存退出.
  * 逐个修改 commit 信息.
* 修改提交者的信息 <https://cloud.tencent.com/developer/article/1393449>

### `git pull --rebase` 冲突解决

```bash
git pull --rebase
# 发现冲突
# 解决冲突
git add .
git rebase --continue
git push
```

### 多个 git 账户 ssh 配置

1. 为每个账户生成 ssh 公钥和私钥

    ```bash
    cd ~/.ssh/

    # github, key 存储文件名输入 id_rsa_github
    ssh-keygen -t rsa -C chenlei.here@qq.com

    # gitee, key 存储文件名输入 id_rsa_gitee
    ssh-keygen -t rsa -C chenlei.here@qq.com
    ```

2. 配置 config 文件

    ```bash
    touch config
    # config 文件内容如下
    # Host github.com
    #     HostName github.com
    #     IdentityFile ~/.ssh/id_rsa_github
    #     User HereChen

    # Host gitee.com
    #     HostName gitee.com
    #     IdentityFile ~/.ssh/id_rsa_gitee
    #     User HereChen
    ```

3. keychain 将 key 添加到 agent (避免 ssh-agent ssh-add 的方式添加) [QuickTips](https://help.ubuntu.com/community/QuickTips)

    ```bash
    sudo apt install keychain
    # zsh 下修改 vim ~/.zshrc
    vim ~/.bashrc
    # keychain id_rsa_github id_rsa_gitee
    # . ~/.keychain/`uname -n`-sh

    source ~/.bashrc
    ```

* 如果报错 `* Error: Problem adding; giving up` 或者类似 `Permissions 0755 for '/home/chen/.ssh/id_rsa' are too open.`，则更改文件夹下所有文件权限。

    ```bash
    chmod -R 700 ~/.ssh
    ```

* WSL 在系统盘之外 git clone 出现各种问题（SSH 已添加成功，代码拉不下来），回到 wsl 的系统内则可以。

### Git 别名

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.pu push
```

### push 默认设置

git 2.x push 默认会推送所有分支，设置为推送当前分支。

```bash
git config --global push.default simple
```

### 修改 git 默认编辑器

```bash
git config --global core.editor vim
```

### 关闭忽略大小写敏感

直接更改文件名大小写，git 不会跟踪，可以关闭大小写忽略。或者用 `git mv` 重命名。

```bash
git config core.ignorecase false
```

### 子模块 (submodules)

```bash
https://git-scm.com/book/en/v2/Git-Tools-Submodules

# 子模块添加
git submodule add https://github.com/chaconinc/DbConnector localfolder_path

# 子模块更新
git submodule update --remote

# 删除子模块的修改
git submodule foreach git reset --hard

# 删除所有子模块的修改
git submodule foreach --recursive git reset --hard
```

## 添加两个源

```bash
git remote add origin 仓库1
git remote add repo2 仓库2
git remote -v

# 从仓库2 pull
git pull repo2
# push 到仓库1
git push origin
# push 到仓库2
git push repo2
```

## 参考资料

* [https://github.com/progit/progit](https://github.com/progit/progit)

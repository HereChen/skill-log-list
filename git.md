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
- 仓库中文件的三种状态：已提交(committed)--本地仓库，已修改(modified)--暂存区域、已暂存(staged)--工作目录。
- 初始化。初始化后会在工作目录中生成 `.git` 目录 。

        ```bash
        git init
        ```

- 跟踪文件。把跟踪文件纳入版本控制。

        ```bash
        git add -A
        ```

- 提交更新。提交更改注释。

        ```bash
        git commit -m "changes for commit"
        ```

- 克隆。克隆仓库到本地。

        ```bash
        git clone git://github.com/schacon/grit.git
        ```

- 查看状态。查看当前文件状态。

        ```bash
        git status
        ```

- 上传。上传至服务器。

        ```bash
        git push -u master
        ```

- 更新查看。查看尚未更新的文件更新的部分。

        ```bash
        git diff
		```

- 移除文件。将文件从已跟踪文件清单移除。

        ```bash
        git rm filename
        ```

- 重命名文件。

        ```bash
        git mv file_from file_to
        ````

- 查看提交历史。

        ```bash
        git log
        ```

- 查看 Git 设置。

        ```bash
        git config --list
        ```

- 启动图形化界面。

        ```bash
        gitk
        ```

- 重新提交(修改最后一次提交)。比如刚提交，但是又忘了将几个文件纳入跟踪，此时可用。

        ```bash
        git commit --amend
        ```

- 取消暂存。在 add 后执行此条，则提交时将不包含此文件的更新。

        ```bash
        git reset HEAD filename
        ```

- 取消修改。

        ```bash
        git checkout -- filename
        ```

- 忽略文件。将不加入版本控制的文件在 `.gitignore` 文件中列出。
- 新建分支: `git checkout -b hunan`
- 清空 git 目录: `git clean -d -x -f`, `-x` 会删除 ignore 的文件 <http://stackoverflow.com/questions/673407/how-do-i-clear-my-local-working-directory-in-git>

- 关闭 `warning: LF will be replaced by CRLF` 警告, `git config --global core.safecrlf false`
- 设置当前 Repo 的账户

        ```bash
        git config user.name "HereChen"
        git config user.email "chenlei.here@qq.com"
        ```

### 合并分支(develop 合并到 master)

pull -> merge -> 修改冲突

1. 切换到 master 分支: git checkout master
2. 合并 develop 到 master: git merge develop
3. 提交(git bash 中 Esc+Shift, wq 保存退出), git push 上传

### Tips

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

### commit

1. 修改提交的信息: `git commit --amend`

## 参考资料

- [https://github.com/progit/progit](https://github.com/progit/progit)

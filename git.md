# Git 学习笔记

1. 公司 Git 与 Github 同时使用: Windows 10 + Ubuntu Bash

## Git 基础

- 仓库中文件的三种状态：已提交(committed)--本地仓库，已修改(modified)--暂存区域、已暂存(staged)--工作目录。
- 初始化。初始化后会在工作目录中生成 `.git` 目录 。

		$ git init

- 跟踪文件。把跟踪文件纳入版本控制。

		$ git add -A

- 提交更新。提交更改注释。

		$ git commit -m "changes for commit"

- 克隆。克隆仓库到本地。

		$ git clone git://github.com/schacon/grit.git

- 查看状态。查看当前文件状态。

		$ git status

- 上传。上传至服务器。

		$ git push -u master

- 更新查看。查看尚未更新的文件更新的部分。

		$ git diff

- 移除文件。将文件从已跟踪文件清单移除。

		$ git rm filename

- 重命名文件。

		$ git mv file_from file_to

- 查看提交历史。

		$ git log

- 查看 Git 设置。

		$ git config --list

- 启动图形化界面。

		$ gitk

- 重新提交(修改最后一次提交)。比如刚提交，但是又忘了将几个文件纳入跟踪，此时可用。

		$ git commit --amend

- 取消暂存。在 add 后执行此条，则提交时将不包含此文件的更新。

		$ git reset HEAD filename

- 取消修改。

		$ git checkout -- filename

- 忽略文件。将不加入版本控制的文件在 `.gitignore` 文件中列出。
- 新建分支: `git checkout -b hunan`
- 清空 git 目录: `git clean -d -x -f`, `-x` 会删除 ignore 的文件 <http://stackoverflow.com/questions/673407/how-do-i-clear-my-local-working-directory-in-git>

- 关闭 `warning: LF will be replaced by CRLF` 警告, `git config --global core.safecrlf false`
- 设置当前 Repo 的账户

	```shell
	git config user.name "HereChen"
	git config user.email "chenlei.here@qq.com"
	```

### 合并分支(develop 合并到 master)

pull -> merge -> 修改冲突

- 切换到 master 分支: git checkout master
- 合并 develop 到 master: git merge develop
- 提交(git bash 中 Esc+Shift, wq 保存退出), git push 上传

## Git 别名

```bash
git config --global alias.co checkout
git config --global alias.br branch
git config --global alias.ci commit
git config --global alias.st status
git config --global alias.pu push
```

## push 默认设置

git 2.x push 默认会推送所有分支，设置为推送当前分支。

```bash
git config --global push.default simple
```

## 参考资料

- [https://github.com/progit/progit](https://github.com/progit/progit)

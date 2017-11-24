# jenkins checkstyle

http://172.23.24.68:8080/

refer:
1. [Jenkins Gitlab持续集成打包平台搭建](http://skyseraph.com/2016/07/18/Tools/Jenkins%20Gitlab%E6%8C%81%E7%BB%AD%E9%9B%86%E6%88%90%E6%89%93%E5%8C%85%E5%B9%B3%E5%8F%B0%E6%90%AD%E5%BB%BA/)

## 启用

```
curl -o jenkins.war https://mirrors.tuna.tsinghua.edu.cn/jenkins/war-stable/2.46.3/jenkins.war
nohup java -jar jenkins.war &
```

## 配置进入

1. localhost:8080 进入
2. Gitlab Authentication plugin 插件安装: Manage Jenkins > Manage Plugins > Avaliable > Gitlab Authentication plugin 
3. SSH 配置: Credentials > ... > Private Key, Enter directly 添加服务器上 ssh-keygen 生成的 private key.
4. 新建 job: 配置 git repo、对应 Credentials、执行的任务.

## 任务配置

- 配置 git repo 和分支
- 配置任务执行触发条件.
- 配置执行的命令.
- 配置任务执行完成后操作: Checkstyle(`**/target/checkstyle-result.xml`), Findbugs(`**/target/findbugsXml.xml`)

## 前端任务配置

缺乏配置, 执行 npm gulp 等命令会提示 `npm command not found`.

- 安装 Nodejs Plugin
- jenkins 服务器上安装 nodejs
- Manage Jenkins > Global Tool Configuration > Add NodeJS > 取消 Install automatically 勾选 > 填写服务器 nodejs 安装目录.
- 任务配置中`Build Environment`勾选`Provide Node & npm bin/ folder to PATH`, 并在`NodeJS Installation`处选择配置的 nodejs

## 插件

1. Gitlab Authentication plugin
2. Checkstyle Plugin
3. FindBugs Plugin
4. Nodejs Plugin

## 重启

8080/restart

todo:
BOSS job, java 代码检查, 前端代码检查.


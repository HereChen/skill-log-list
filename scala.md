# Scala

> <https://www.scala-lang.org>

## 安装（Ubuntu/Debian）

```bash
# https://docs.scala-lang.org/getting-started/sbt-track/getting-started-with-scala-and-sbt-on-the-command-line.html
# https://gist.github.com/Frozenfire92/3627e38dc47ca581d6d024c14c1cf4a9

## java
# !安装失败
sudo apt-get update
sudo apt-get install default-jdk
java --version

## sbt
# https://www.scala-sbt.org/1.x/docs/Installing-sbt-on-Linux.html
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
curl -sL "https://keyserver.ubuntu.com/pks/lookup?op=get&search=0x2EE0EA64E40A89B84B2DF73499E82A75642AC823" | sudo apt-key add
sudo apt-get update
sudo apt-get install sbt

# 如果无法下载 sbt，可以手动下载后安装
# https://dl.bintray.com/sbt/debian/sbt-1.3.10.deb
# sudo dpkg -i sbt-1.3.10.deb

sbt --version
```

## Hello World

> <https://docs.scala-lang.org/getting-started/sbt-track/getting-started-with-scala-and-sbt-on-the-command-line.html>

```bash
sbt new scala/hello-world.g8
cd hello-world
sbt
~run
```

**备注** 如果执行 sbt 下载失败

```bash
cd ~/.sbt
touch repositories
vim repositories
# 填入下面的内容
```

```
[repositories]
local
aliyun: https://maven.aliyun.com/repository/public
huaweicloud-maven: https://repo.huaweicloud.com/repository/maven/
jcenter: https://jcenter.bintray.com
maven-central: https://repo1.maven.org/maven2/
typesafe: https://repo.typesafe.com/typesafe/ivy-releases/, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext], bootOnly
sbt-plugin-repo: https://repo.scala-sbt.org/scalasbt/sbt-plugin-releases, [organization]/[module]/(scala_[scalaVersion]/)(sbt_[sbtVersion]/)[revision]/[type]s/[artifact](-[classifier]).[ext]
```

* <https://blog.csdn.net/binbinczsohu/article/details/105289456>
* <https://help.aliyun.com/document_detail/102512.html>

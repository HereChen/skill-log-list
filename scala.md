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

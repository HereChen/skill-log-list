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

* [Proxy Repositories](https://www.scala-sbt.org/1.x/docs/Proxy-Repositories.html)
* <https://blog.csdn.net/binbinczsohu/article/details/105289456>
* <https://help.aliyun.com/document_detail/102512.html>

## Demo (Spark)

> <https://spark.apache.org/docs/latest/quick-start.html>

```scala
// README.md 中 a 和 b 的行数
import org.apache.spark.sql.SparkSession

object Main extends App {
  val logFile = "/home/chen/practice/scala/README.md" // Should be some file on your system
  val spark = SparkSession
    .builder
    .appName("Simple Application")
    .config("spark.master", "local")
    .getOrCreate()
  val logData = spark.read.textFile(logFile).cache()
  val numAs = logData.filter(line => line.contains("a")).count()
  val numBs = logData.filter(line => line.contains("b")).count()
  println(s"Lines with a: $numAs, Lines with b: $numBs")
  spark.stop()
}
```

```scala
scalaVersion := "2.12.10"
name := "hello-world"
organization := "ch.epfl.scala"
version := "1.0"
libraryDependencies ++= Seq(
  "org.apache.spark" %% "spark-sql" % "2.4.5"
)
```

## sbt

[sbt](./sbt.md)

## Maven

example <https://github.com/jesperdj/scala-maven-example>，依赖 `scala-maven-plugin` 和 `maven-assembly-plugin` 打包（包含依赖）。

```xml
<!-- 只包含 build 部分 -->
<build>
  <plugins>
    <!-- Scala support -->
    <plugin>
      <groupId>net.alchim31.maven</groupId>
      <artifactId>scala-maven-plugin</artifactId>
      <version>4.3.1</version>
      <executions>
        <execution>
          <goals>
            <goal>compile</goal>
          </goals>
        </execution>
      </executions>
    </plugin>
    <!-- scala assembly -->
    <plugin>
      <groupId>org.apache.maven.plugins</groupId>
      <artifactId>maven-assembly-plugin</artifactId>
      <version>2.4</version>
      <configuration>
        <descriptorRefs>
          <descriptorRef>jar-with-dependencies</descriptorRef>
        </descriptorRefs>
        <archive>
          <manifest>
            <mainClass>Main</mainClass>
          </manifest>
        </archive>
      </configuration>
      <executions>
          <execution>
              <phase>package</phase>
              <goals>
                  <goal>single</goal>
              </goals>
          </execution>
      </executions>
    </plugin>
  </plugins>
</build>
```

## Tips

### IntelliJ IDEA

* 安装 Scala 插件。
* 配置 `.sbt/repositories` 文件。
* sbt shell, loading sbt plugins 报错 `wrong checksum` 时，手动下载 jar 包替换。

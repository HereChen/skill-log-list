# sbt

> <https://www.scala-sbt.org>

## command

通过 sbt 执行，或者先执行 sbt 进入交互式命令，输入命令。

```bash
# 方法1: sbt [命令]
sbt package
# 方法2
sbt
> package
```

```bash
console     # console 模式，可进行交互式计算
run         # 启动工程
~run        # 启动工程并检测代码变更
package     # 打包
reload      # 刷新代码(进入交互命令，不会自动使用最新的代码)
makePom     # 生成 pom 文件
```

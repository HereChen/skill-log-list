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
console               # console 模式，可进行交互式计算
run                   # 启动工程
~run                  # 启动工程并检测代码变更
reload                # 重新加载编译配置(进入交互命令，不会自动使用最新的代码)
makePom               # 生成 pom 文件
runMain example.Main  # 执行指定的类，后面可空格接参数
show discoveredMainClasses
test                  # 执行测试用例
projects              # 查看当前工程所有子项目
project projectName   # 工程切换
clean                 # 清除 target
compile               # 编译 main sources
package               # 打包
update                # 更新依赖
```

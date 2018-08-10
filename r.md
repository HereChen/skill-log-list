# R

> R 语言

1. <https://www.r-project.org/>
2. <https://www.rstudio.com/>
3. [cheatsheet](https://www.rstudio.com/resources/cheatsheets/)

## 常用命令

```bash
# 清除 x 和 y 在工作空间中的数据
rm(x, y)

# 清除所有数据
rm(list=ls())

# 保存工作空间, 参数可为保存的文件路径
save.image()
```

## 基本用法

- 安装包: `install.packages("rjson")`
- 赋值: `a <- 2`
- 向上一层作用于赋值: `a <<- 2`
- 删除变量: `rm(a)`

## 数据类型

- 向量: `x <- c(1,5,8,9,1,2,5)`
- 矩阵: `x <- matrix(1:10, 2, 5)`
- 数组, array(data, dim): `x <- array(1:10, c(2,5))`

## 绘图

- 柱状图: `barplot(c(2,3,4,5))`

## JSON 处理

```bash
install.packages("rjson")
```

```r
library('rjson')
setwd('设置工作路径')
result <- fromJSON(file = 'data.json')
print(result)
```

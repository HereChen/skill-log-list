# R

> R 语言

1. <https://www.r-project.org/>
2. <https://www.rstudio.com/>
3. [cheatsheet](https://www.rstudio.com/resources/cheatsheets/)

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

```r
install.packages("rjson")
```
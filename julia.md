# julia

> <https://julialang.org/>

## 安装

```bash
# https://subscription.packtpub.com/book/application_development/9781788998369/1/ch01lvl1sec12/installing-julia-from-binaries
# https://blog.simos.info/learning-the-julia-computer-language-on-ubuntu/
wget https://julialang-s3.julialang.org/bin/linux/x64/1.1/julia-1.1.1-linux-x86_64.tar.gz
tar xvf julia-1.1.1-linux-x86_64.tar.gz

# 环境环境变量设置
echo PATH=\$PATH:~/julia-1.1.1/bin/ >> ~/.barshrc
source ~/.barshrc

julia -version
```

## IDE

1. [Juno](https://junolab.org)
2. [JuliaPro](https://juliacomputing.com/products/juliapro.html)

## 基础

* 文件后缀 `.jl`。
* Unicode 可以作为变量 `δ = √2`。
* 添加、删除、更新包

    ```julia
    using Pkg
    Pkg.add("Plots")
    Pkg.update("Plots")
    Pkg.rm("Plots")
    ```

```julia
# 一个简单的示例
# main.jl
x = 10;
println(x);
```

```julia
# 允许 Markdown 注释
"""
这里注释
"""
```

```bash
# 终端中执行
julia main.jl
```

## 模块

```julia
# demo.jl
include("./basic-demo.jl")
@time MatrixDemo.print();
```

```julia
module MatrixDemo
    using LinearAlgebra

    function print()
      println("\nMatrixDemo");

      A = [1 2 3; 4 1 6; 7 8 1];
      println(det(A)) # 行列式
      println(inv(A)) # 取逆矩阵
    end
end
```

## 资料

1. [Julia, my new friend for computing andoptimization?, Pierre Haessig, Lilian Besson, 2018](https://hal.archives-ouvertes.fr/cel-01830248/document)

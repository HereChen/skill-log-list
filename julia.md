# julia

> <https://julialang.org/>

## 安装

```bash
cd /opt
# https://subscription.packtpub.com/book/application_development/9781788998369/1/ch01lvl1sec12/installing-julia-from-binaries
# https://blog.simos.info/learning-the-julia-computer-language-on-ubuntu/
wget https://julialang-s3.julialang.org/bin/linux/x64/1.3/julia-1.3.1-linux-x86_64.tar.gz
tar xvf julia-1.3.1-linux-x86_64.tar.gz

# 环境环境变量设置
vim ~/.barshrc
# export JULIA_HOME=/opt/julia-1.3.1
# export PATH=$JULIA_HOME/bin:$PATH
source ~/.barshrc

julia -version
```

## IDE

1. [Juno](https://junolab.org)
2. [JuliaPro](https://juliacomputing.com/products/juliapro.html)
3. [Jupyter](https://jupyter.org/install.html) `pip install jupyterlab -i https://pypi.douban.com/simple`

## 执行

```bash
# 在 bash 中执行
$ julia filename.jl

# 在 julia repl 中执行
julia> 1 + 1
# https://stackoverflow.com/a/22241095
julia> include("C:\Users\chenl\.julia\packages\FFMPEG\9JQpZ\deps\build.jl")
```

## 基础

* 文件后缀 `.jl`。
* Unicode 可以作为变量 `δ = √2`。
* 添加、删除、更新包

    ```julia
    using Pkg
    Pkg.add("Plots")
    Pkg.update("Plots")
    Pkg.rm("Plots")

    # 安装失败重新安装。有时候下载依赖会失败，可以根据错误，将依赖中的包手动下载下来放入对应的文件夹（build 文件也可能需要手动下载）
    Pkg.rm("Plots")
    Pkg.gc()
    Pkg.add("Plots")
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

## 绘图

```julia
using Plots

include("./findzero.jl");

x0 = 10;
f(x) = x^2 - 2;
x = FindZero.newton(f, x0);

plot(f, 0, x0 + 1);
# 在上面图的基础上绘制
plot!(x, f.(x), legend=false, shape = [:circle]);
plot!([x[end]], [f(x[end])], shape = [:utriangle], markersize=6);
```

## 资料

1. [Julia, my new friend for computing andoptimization?, Pierre Haessig, Lilian Besson, 2018](https://hal.archives-ouvertes.fr/cel-01830248/document)

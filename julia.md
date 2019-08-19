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

## 基础

```julia
# main.jl
x = 10;
println(x);
```

```bash
julia main.jl
```

## 资料

1. [Julia, my new friend for computing andoptimization?, Pierre Haessig, Lilian Besson, 2018](https://hal.archives-ouvertes.fr/cel-01830248/document)
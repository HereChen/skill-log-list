# Webassembly

Go 语言上手 demo 比较容易. Emscripten 工具不易安装成功.

## Tools

* [Emscripten](https://github.com/emscripten-core/emscripten): C/C++ -> Webassembly
* [MATLAB Coder](https://www.mathworks.com/products/matlab-coder.html): MATLAB -> C/C++
* [AssemblyScript](https://github.com/AssemblyScript/assemblyscript): TypeScript -> Webassembly
* [Go's Assembler](https://golang.org/doc/asm): golang -> Webassembly
* [Blazor](https://github.com/aspnet/Blazor): C# -> Webassembly
* [Rust and WebAssembly](https://github.com/rustwasm): Rust -> Webassembly

### Emscripten

> <https://emscripten.org>

**install (directly)**: emscripten

```bash
git clone https://github.com/emscripten-core/emsdk.git

cd emsdk
# 修改 emsdk 文件下载逻辑, 从 taobao 下载 nodejs
# print("Installing tool '" + str(self) + "'..")
# url = self.download_url()

# if url == "node-v8.9.1-linux-x64.tar.xz":
#  print("nodejs.......")
#  url = 'https://npm.taobao.org/mirrors/node/latest-v8.x/node-v8.9.1-linux-x64.tar.xz'

./emsdk install latest

./emsdk activate latest

# 每次重启 terminal 都要执行
source ./emsdk_env.sh

# 验证安装
emcc -v
em++ -v
```

tips: `lkgr.json` 下载失败, 可手动下载后复制到 `upstream` 文件下.

**install (docker)** 用 docker 安装工具.

1. [Building projects on Travis CI](https://emscripten.org/docs/compiling/Travis.html)
2. [trzeci/emscripten - Docker Hub](https://hub.docker.com/r/trzeci/emscripten)

```bash
# download
docker pull trzeci/emscripten

# enter docker container
docker run -t -i trzeci/emscripten /bin/bash

# 进入后查看版本
emcc --version

# 使用 docker 内 emsdk
docker run --rm -v $(pwd):/src trzeci/emscripten emcc helloworld.cpp -o helloworld.js
```

**demo**: `hello_world.c`

```c
/*
 * Copyright 2011 The Emscripten Authors.  All rights reserved.
 * Emscripten is available under two separate licenses, the MIT license and the
 * University of Illinois/NCSA Open Source License.  Both these licenses can be
 * found in the LICENSE file.
 */

#include <stdio.h>

int main() {
  printf("hello, world!\n");
  return 0;
}
```

```bash
# https://emscripten.org/docs/compiling/Building-Projects.html#emscripten-build-output-files
# 编译
emcc hello_world.c
emcc hello_world.c -o hello.wasm
# 生成 wasm 和 对应运行的 js
emcc hello_world.c -o hello.js

# node 执行
node a.out.js

# 生成 html 运行模板
emcc hello_world.c -o hello.html
```

加载 emcc 生成的 js 后, 可通过 Module.asm 查看暴露的函数.

**wabt** wat(具有可读性的文件) 和 wasm 格式转换工具.

```bash
git clone --recursive git@github.com:WebAssembly/wabt.git
cd wabt
mkdir build
cd build
cmake ..
make

wat2wasm test.wat -o test.wasm
wasm2wat test.wasm -o test.wat
```

**JS 传数组或矩阵到 C/C++** TODO:

需要将数组转换成 Type Array, 比如 Float32Array. Webassembly 可以接收的类型?

1. [glmw](https://github.com/maierfelix/glmw/)
2. [Passing and returning WebAssembly array parameters](https://becominghuman.ai/passing-and-returning-webassembly-array-parameters-a0f572c65d97)
3. [C++ to WebAssembly: Pass arrays to C++](https://medium.com/@tdeniffel/c-to-webassembly-pass-and-arrays-to-c-86e0cb0464f5)

### MATLAB > C/C++ > Webassembly

MATLAB 并不直接编译成 Webassembly, 但可以利用其编译成 C/C++ 的能力, 再利用 Emscripten 编译成 Webassembly. 流程:

1. **代码生成**: (Windows) MATLAB Coder 工具, 将 MATLAB 代码编译成 C/C++. 生成的代码会包含 *.mk 文件, 为 Makefile 文件. 编译时如果选择 MATLAB host (当前电脑的环境), 会同时生成 *.bat 文件.
2. **编译获取 lib 文件**: 运行 *.bat 文件生成 *.lib 文件.
3. **编写程序**: 引入 *.lib 文件编写程序. (TODO: lib 是 Windows平台的静态链接库, 须在 Windows 平台编译)
4. **编译成 Webassembly**: 利用 Emscripten 编译.

* [Automatically Converting MATLAB Code to C Code](https://www.mathworks.com/videos/automatically-converting-matlab-code-to-c-code-96483.html)

## Examples

**导出 C++ 方法** JavaScript 调用 C++ 方法.

```c++
// export_cpp_method.cpp
// https://emscripten.org/docs/porting/connecting_cpp_and_javascript/embind.html
#include <emscripten.h>
#include <emscripten/bind.h>

double sum(double a, double b) {
  return a + b;
}

// 导出 sum
EMSCRIPTEN_BINDINGS(my_module){
    emscripten::function("sum", &sum);
}
```

```bash
em++ -std=c++11 --bind -o export_cpp_method.js export_cpp_method.cpp
# docker run --rm -v $(pwd):/src trzeci/emscripten em++ -std=c++11 --bind -o export_cpp_method.js export_cpp_method.cpp
```

```html
<!-- export_cpp_method.html -->
<!doctype html>
<html>
  <script>
    var Module = {
      onRuntimeInitialized: function() {
        console.log('sum result: ' + Module.sum(2, 3));
      }
    };
  </script>
  <script src="export_cpp_method.js"></script>
</html>
```

## Tips

### 加载后回调/`onRuntimeInitialized`

> <https://emscripten.org/docs/getting_started/FAQ.html>

* 一种是提前定义 `onRuntimeInitialized`，见上面的 Example。
* 通过 Promise 方式回调。编译时加参数 `-s MODULARIZE=1 -s 'EXPORT_NAME="createMyModule"'`，可参考 [squoosh/codecs/mozjpeg_enc/build.sh](https://github.com/GoogleChromeLabs/squoosh/blob/ff7dc2c4cf0f080fef7e172c4b0ff6f4a1dd7e63/codecs/mozjpeg_enc/build.sh#L33)。

```js
createMyModule(/* optional default settings */).then(function(Module) {
  // Module 是暴露的模块，这里回调
});
```

## Use Case

* [fastq.bio, How We Used WebAssembly To Speed Up Our Web App By 20X (Case Study)](https://www.smashingmagazine.com/2019/04/webassembly-speed-web-app/)
* [Figma, WebAssembly cut Figma's load time by 3x](https://www.figma.com/blog/webassembly-cut-figmas-load-time-by-3x/)
* [brion/ogv.js](https://github.com/brion/ogv.js): 音视频播放器.
* [Web端H.265播放器研发解密, 淘宝技术](https://mp.weixin.qq.com/s/ajLFM8q-4-2hxj-M_ChGdg)
* [ColinEberhardt/wasm-mandelbrot](https://github.com/ColinEberhardt/wasm-mandelbrot) 分形图几种实现方式的对比。
* [WebAssembly at eBay: A Real-World Use Case](https://tech.ebayinc.com/engineering/webassembly-at-ebay-a-real-world-use-case/)
* [GoogleChromeLabs/squoosh](https://github.com/GoogleChromeLabs/squoosh) 图片压缩。

## Readings

* [Build your own WebAssembly Compiler, Colin Eberhardt, 2019-05-17](https://blog.scottlogic.com/2019/05/17/webassembly-compiler.html)
* [前端核心代码保护技术面面观](https://zhuanlan.zhihu.com/p/61651310)
* [Compiling C to WebAssembly without Emscripten, Surma, 2019-05-28](https://dassur.ma/things/c-to-webassembly/)
* [WebAssembly Is Fast: A Real-World Benchmark of WebAssembly vs. ES6](https://medium.com/@torch2424/webassembly-is-fast-a-real-world-benchmark-of-webassembly-vs-es6-d85a23f8e193)

## Appendix

### emsdk

```bash
.
├── Dockerfile
├── LICENSE
├── README.md
├── bin
│   └── elevate.exe
├── binaryen-tags.txt
├── clang
│   ├── fastcomp
│   │   ├── build_incoming_64
│   │   └── src
│   └── tag-e1.38.29
│       ├── build_tag-e1.38.29_64
│       └── src
├── emcmdprompt.bat
├── emscripten-tags.txt
├── emsdk
├── emsdk.bat
├── emsdk.ps1
├── emsdk_env.bat
├── emsdk_env.ps1
├── emsdk_env.sh
├── emsdk_manifest.json
├── emsdk_set_env.sh
├── fastcomp
│   └── 3941
│       ├── Wack.cmake
│       ├── bin
│       ├── cmake
│       ├── emscripten
│       ├── emscripten_config
│       ├── emscripten_config_sanity
│       ├── emscripten_config_vanilla
│       ├── emscripten_config_vanilla_sanity_wasm
│       ├── fastcomp
│       ├── include
│       ├── lib
│       ├── libexec
│       ├── share
│       └── sysroot
├── node
│   └── 8.9.1_64bit
│       ├── CHANGELOG.md
│       ├── LICENSE
│       ├── README.md
│       ├── bin
│       ├── etc
│       ├── include
│       ├── lib
│       └── share
├── tree.md
├── upstream
│   └── lkgr.json
└── zips
    ├── 3941-wasm-binaries.tbz2
    ├── clang-e1.38.29.tar.gz
    ├── llvm-e1.38.29.tar.gz
    └── node-v8.9.1-linux-x64.tar.xz
```

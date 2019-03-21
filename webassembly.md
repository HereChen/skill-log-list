# Webassembly

Go 语言上手 demo 比较容易. Emscripten 工具不易安装成功.

## Emscripten

> <https://emscripten.org>

**install**: emscripten

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
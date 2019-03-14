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

source ./emsdk_env.sh

# 验证安装
emcc -v
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
# 编译
emcc hello_world.c

# node 执行
node a.out.js

# 生成 html 运行模板
emcc hello_world.c -o hello.html
```
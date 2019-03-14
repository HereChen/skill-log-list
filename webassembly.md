# Webassembly

Go 语言上手 demo 比较容易. Emscripten 工具不易安装成功.

## Emscripten

> <https://emscripten.org>

```bash
git clone https://github.com/emscripten-core/emsdk.git

cd emsdk
./emsdk install latest

./emsdk activate latest

# nodejs installed by nvm
sudo ln -s /home/chen/.nvm/versions/node/v8.9.1/bin/node /usr/local/bin/node
sudo ln -s /home/chen/.nvm/versions/node/v8.9.1/bin/npm /usr/local/bin/npm

vim ~/.emscripten
# NODE_JS = '/usr/local/bin/node'
```

tips: 忽略 nodejs 下载错误, 采用系统已有的; `lkgr.json` 下载失败, 可手动下载后复制到 `upstream` 文件下.
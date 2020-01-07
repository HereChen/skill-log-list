# nodejs

## 安装

安装的方式包括: 从源码编译安装, 直接下载二进制, 依靠工具直接从库下载安装。

**Linux 编译安装**

```bash
curl -o node-v10.0.0.tar.gz https://nodejs.org/dist/latest/node-v10.0.0.tar.gz
tar -xvzf node-v10.0.0.tar.gz
cd node-v10.0.0
./configure
make
make install
```

**Linux 安装二进制文件**

```bash
# 64bit node install
curl -o node-v6.10.0-linux-x64.tar.xz https://nodejs.org/dist/v6.10.0/node-v6.10.0-linux-x64.tar.xz
tar -xvJf node-v6.10.0-linux-x64.tar.xz
mv node-v6.10.0-linux-x64 node

vi ~/.bash_profile
# 添加以下内容到 .bash_profile
# export NODE_HOME=/opt/node
# export PATH=$NODE_HOME/bin:$PATH
source ~/.bash_profile

node -v
```

**Ubuntu 安装**

ubuntu 安装 nodejs, <https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions>

```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```

## Tips

* 执行本地命令, <http://stackoverflow.com/questions/20643470/execute-a-command-line-binary-with-node-js>
* node_modules windows 上删除

    ```bash
    npm install -g rimraf
    rimraf node_modules
    ```

* Ubuntu Bash 中 npm command not found

    ```bash
    sudo chmod 755 -R /usr/local/node/bin
    sudo ln -s /usr/local/node/bin/node /usr/bin/node
    sudo ln -s /usr/local/node/lib /usr/lib/node
    sudo ln -s /usr/local/node/bin/npm /usr/bin/npm
    ```

* ES Modules 执行(mjs 后缀): `node --experimental-modules app.js`

## 版本切换(nvm)

```bash
# 安装 nvm
wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.35.2/install.sh | bash

# 安装 nodejs
nvm install v8.12.0

# 切换版本
nvm use v8.12.0

# 设置默认版本
nvm alias default v10.10.0
```

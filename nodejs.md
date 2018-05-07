# nodejs

* 执行本地命令, <http://stackoverflow.com/questions/20643470/execute-a-command-line-binary-with-node-js>
* node_modules windows 上删除

    ```bash
    npm install -g rimraf
    rimraf node_modules
    ```

## 安装

### Linux 安装

```bash
curl -o node-v10.0.0.tar.gz https://nodejs.org/dist/latest/node-v10.0.0.tar.gz
tar -xvzf node-v10.0.0.tar.gz
cd node-v10.0.0
./configure
make
make install
```

### Ubuntu 安装

ubuntu 安装 nodejs, <https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions>

```bash
curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
sudo apt-get install -y nodejs
```
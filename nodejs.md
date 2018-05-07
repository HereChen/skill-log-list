/*
 * @Author: chenlei 
 * @Date: 2017-03-10 14:10:01 
 * @Last Modified by:   chenlei 
 * @Last Modified time: 2017-03-10 14:10:01 
 */

# nodejs

* 执行本地命令, <http://stackoverflow.com/questions/20643470/execute-a-command-line-binary-with-node-js>
* ubuntu 安装 nodejs, <https://nodejs.org/en/download/package-manager/#debian-and-ubuntu-based-linux-distributions>

    ```bash
    curl -sL https://deb.nodesource.com/setup_6.x | sudo -E bash -
    sudo apt-get install -y nodejs
    ```

* node_modules windows 上删除

    ```bash
    npm install -g rimraf
    rimraf node_modules
    ```
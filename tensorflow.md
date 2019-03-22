# TensorFlow

> <https://www.tensorflow.org> An end-to-end open source machine learning platform.

## Docker

**安装方式1: 从 `hub.docker.com` 安装** 默认方式安装

```bash
# https://www.tensorflow.org/install#run-a-tensorflow-container
docker pull tensorflow/tensorflow                  # Download latest image
docker run -it -p 8888:8888 tensorflow/tensorflow  # Start a Jupyter notebook server
```

**安装方式2: 从 `daocloud.io` 安装** 上面的方式很可能装不上, 可用 daocloud

```bash
docker pull daocloud.io/daocloud/tensorflow:latest
docker run -it -p 8888:8888 daocloud.io/daocloud/tensorflow:latest
```

**安装方式3: 设置镜像安装** daocloud 安装的很可能不是最新版本, 可更改 mirror 地址

```bash
touch /etc/docker/daemon.json
```

向 `/etc/docker/daemon.json` 文件添加如下内容

```json
{
  "registry-mirrors": ["https://registry.docker-cn.com"]
}
```

```bash
# https://docs.docker.com/registry/recipes/mirror/#use-case-the-china-registry-mirror
# https://yeasy.gitbooks.io/docker_practice/content/install/mirror.html
systemctl stop docker
systemctl start docker

docker pull tensorflow/tensorflow
docker run -it -p 8888:8888 tensorflow/tensorflow

# 安装 2.0
# sudo docker pull tensorflow/tensorflow:2.0.0a0-py3-jupyter
```

## 使用

```bash
# 查看 tensorflow 版本
pip list | grep tensorflow
```
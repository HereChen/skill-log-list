# Docker

> [docs.docker.com](https://docs.docker.com)

## 安装(CentOS)

```bash
# Install using the repository
sudo yum install -y yum-utils \
  device-mapper-persistent-data \
  lvm2

# 官方的镜像会下载超时，换成中科大的镜像
# 官方镜像 https://download.docker.com/linux/centos/docker-ce.repo
sudo yum-config-manager \
  --add-repo \
  https://download.docker.com/linux/centos/docker-ce.repo
sudo yum-config-manager --enable docker-ce-edge
sudo yum-config-manager --enable docker-ce-test
# sudo yum-config-manager --disable docker-ce-edge

# INSTALL DOCKER CE
# 下载超时，则替换 /etc/yum.repos.d/docker-ce.repo 中镜像地址
# https://download.docker.com/linux/centos
# 替换成
# http://mirrors.ustc.edu.cn/docker-ce/linux/centos
sudo yum install docker-ce

sudo systemctl start docker
sudo docker run hello-world
```

## 基本命令

```bash
# 启动
# 停止
```

# Docker

> [docs.docker.com](https://docs.docker.com)
> [docker-cheat-sheet](https://github.com/wsargent/docker-cheat-sheet)

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
# 查看版本
docker --version

# 查看更多详细信息（或者 docker version）
docker info

# 查看运行的实例（container）
docker ps

# 查看下载的 image（container 是 image 的实例）
docker image ls

# 查看 container
docker container ls

# 运行容器
docker run hello-world

# stop container
# 最后一个参数是 container id，可通过 docker container ls 查找
docker container stop 1fa4ab2cf395
```

## 创建 image

> [Get Started, Part 2: Containers](https://docs.docker.com/get-started/part2/)

```bash
# 创建 Dockerfile，并准备应用相关的文件，当前文件夹下执行
docker build -t friendlyhello .

# 查看创建后是否新增 friendlyhello
docker image ls

# 运行（container 内的 80 映射到系统实际可访问的 4000）
# 默认 foreground mode 运行
# detached mode 运行, 即 background 运行: docker run -d -p 4000:80 friendlyhello
docker run -p 4000:80 friendlyhello

# 查看启动的服务
curl http://localhost:4000
```

## Dockerfile

```text
# 指定基础镜像（image）
FROM python:2.7-slim

# 指定指令执行的目录（默认的目录是 /）
WORKDIR /home/demo/docker/python

# 将当前文件夹下的内容复制到 /home/demo/docker/python
ADD . /home/demo/docker/python

# 安装 requirements.txt 中的依赖
RUN pip install --trusted-host pypi.python.org -r requirements.txt

# 将容器内 80 端口暴露给外部（应用的端口）
EXPOSE 80

# 定义环境变量 NAME 的值为 World
ENV NAME World

# 容器启动后执行 python app.py
# 只能有一个指令
CMD ["python", "app.py"]
```

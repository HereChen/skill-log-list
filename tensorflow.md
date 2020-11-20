# TensorFlow

> <https://www.tensorflow.org> An end-to-end open source machine learning platform.  
> <https://tensorflow.google.cn/>

## 安装

```bash
sudo apt install python3
sudo apt install python3-pip

sudo pip install -i https://mirrors.aliyun.com/pypi/simple tensorflow
sudo pip install -i https://mirrors.aliyun.com/pypi/simple tensorflow-cpu
```

demo

```python
# https://github.com/tensorflow/tensorflow#try-your-first-tensorflow-program
import tensorflow as tf

tf.add(1, 2).numpy()
hello = tf.constant('Hello, TensorFlow!')
hello.numpy()
```

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
  "registry-mirrors": ["https://reg-mirror.qiniu.com"]
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
# docker run -it -p 8888:8888 tensorflow/tensorflow:2.0.0a0-py3-jupyter
```

## 使用

```bash
# 查看 tensorflow 版本
pip list | grep tensorflow
```

## Tensorflow Serving

> <https://tensorflow.google.cn/tfx/serving/docker>

```bash
# docker 安装
docker pull tensorflow/serving

# 下载 demo
git clone https://github.com/tensorflow/serving
TESTDATA="$(pwd)/serving/tensorflow_serving/servables/tensorflow/testdata"

# docker 启用服务 （让模型可以通过 REST API 访问）
docker run -t --rm -p 8501:8501 \
    -v "$TESTDATA/saved_model_half_plus_two_cpu:/models/half_plus_two" \
    -e MODEL_NAME=half_plus_two \
    tensorflow/serving &

# 测试接口
curl -d '{"instances": [1.0, 2.0, 5.0]}' \
    -X POST http://localhost:8501/v1/models/half_plus_two:predict
```

```bash
# my model
# 模型路径：/home/chen/workspace/tensorflow-my-model/machin_learning_demo_model/1
sudo docker run -p 8501:8501 \
  --mount type=bind,source=/home/chen/workspace/tensorflow-my-model/machin_learning_demo_model,target=/models/machin_learning_demo_model \
  -e MODEL_NAME=machin_learning_demo_model -t tensorflow/serving &
```
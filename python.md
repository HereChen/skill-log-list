# python

## 安装

```bash
# Ubuntu
sudo apt install python3

# pip 安装
sudo apt install python3-pip
```

## 包管理

```bash
# 安装
pip install matplotlib

# 通过镜像安装
# https://mirrors.tuna.tsinghua.edu.cn/help/pypi/
# 阿里云: https://mirrors.aliyun.com/pypi/simple
# 清华：https://pypi.tuna.tsinghua.edu.cn/simple
pip install -i https://mirrors.aliyun.com/pypi/simple matplotlib

# 升级
pip install -U matplotlib

# 卸载
pip uninstall matplotlib

# 搜索
pip search "matplotlib"
```
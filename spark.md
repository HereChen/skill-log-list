# Apache Spark

## Install

```bash
wget https://mirrors.tuna.tsinghua.edu.cn/apache/spark/spark-2.4.5/spark-2.4.5-bin-hadoop2.7.tgz
sudo tar xvf spark-2.4.5-bin-hadoop2.7.tgz -C /usr/local/spark
vim ~/.bashrc
# SPARK_HOME=/usr/local/spark
# export PATH=$SPARK_HOME/bin:$PATH
source ~/.bashrc
spark-shell
```

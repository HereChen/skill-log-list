# maven

## 安装

```bash
# jdk
sudo wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" http://download.oracle.com/otn-pub/java/jdk/10.0.1+10/fb4372174a714e6b8c52526dc134031e/jdk-10.0.1_linux-x64_bin.tar.gz
tar zxvf jdk-10.0.1_linux-x64_bin.tar.gz
vim ~/.bash_profile
# export JAVA_HOME=/usr/local/jdk-10.0.1
# export PATH=$JAVA_HOME/bin:$JAVA_HOME/jre/bin:$PATH
source ~/.bash_profile

# maven
curl -o apache-maven-3.5.3-bin.tar.gz http://apache.fayea.com/maven/maven-3/3.5.3/binaries/apache-maven-3.5.3-bin.tar.gz
tar zxvf apache-maven-3.5.3-bin.tar.gz

vim ~/.bash_profile
# export M2_HOME=/usr/local/apache-maven-3.5.3
# PATH=$M2_HOME/bin:$PATH
source ~/.bash_profile
```

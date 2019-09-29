# Java

## Environments

**OpenJDK Install (Ubuntu)** two methods below.

```bash
# Method 1.
# apt install default-jdk
# apt-cache search openjdk
apt install openjdk-8-jdk

# Method 2: openjdk 10 manual
# 1. https://jdk.java.net/archive/
# 2. http://openjdk.java.net/install/index.html
# 3. https://stackoverflow.com/questions/49507160/how-to-install-jdk-10-under-ubuntu

wget https://download.java.net/java/GA/jdk10/10.0.2/19aef61b38124481863b1413dce1855f/13/openjdk-10.0.2_linux-x64_bin.tar.gz
tar xzvf openjdk-10.0.2_linux-x64_bin.tar.gz
mv jdk-10.0.2 /usr/lib/jvm/java-10-openjdk-amd64/
update-alternatives --install /usr/bin/java java /usr/lib/jvm/java-10-openjdk-amd64/bin/java 1
update-alternatives --install /usr/bin/javac javac /usr/lib/jvm/java-10-openjdk-amd64/bin/javac 1
update-alternatives --config java
```

**OpenJDK CentOS**

```bash
yum install java-1.8.0-openjdk
```

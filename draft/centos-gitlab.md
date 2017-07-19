# CentOS GitLab CE

## 准备

- 下载安装: <https://about.gitlab.com/installation/#centos-7>

## 安装配置

1. 依赖安装

```bash
sudo yum install curl policycoreutils openssh-server openssh-clients
sudo systemctl enable sshd
sudo systemctl start sshd
sudo yum install postfix
sudo systemctl enable postfix
sudo systemctl start postfix
sudo firewall-cmd --permanent --add-service=http
sudo systemctl reload firewalld
```

2. gitlab-ce 安装

```bash
curl -sS https://packages.gitlab.com/install/repositories/gitlab/gitlab-ce/script.rpm.sh | sudo bash
sudo yum install gitlab-ce
```

3. 配置启动 GitLab

```bash
sudo gitlab-ctl reconfigure
```
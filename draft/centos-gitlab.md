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

4. 备用

```bash
# gitlab-ctl command not found
# refer: https://gitlab.com/gitlab-org/omnibus-gitlab/issues/493
/opt/gitlab/bin/gitlab-ctl reconfigure
# 或者先添加链接 ln -s /opt/gitlab/bin/gitlab-ctl /usr/bin/gitlab-ctl

# gitlab-ctl reconfigure 报错 Chef client failed (ssh)
# Error executing action `run` on resource 'execute[semodule -i /opt/gitlab/embedded/selinux/...ssh-keygen.pp'
# refer: https://gitlab.com/gitlab-org/gitlab-ce/issues/28915
yum install libsemanage-static libsemanage-devel
```

5. localhost 改成 IP

新建项目后, 默认地址是 localhost, 比如: `git@localhost:ProjectsSource/xxxxx.git`. 需要更改配置文件.

```bash
cd /opt/gitlab/embedded/service/gitlab-rails/config  
vim gitlab.yml
# host: localhost 改为 host: 192.168.100.133
```

在浏览器中输入本机 IP 进入 GitLab.

## 使用

- GitLab CE API: <https://docs.gitlab.com/ce/api/>
- gitlab ce ci, <https://docs.gitlab.com/ce/ci/>
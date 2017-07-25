# saltstack

## ubuntu

<https://repo.saltstack.com/#ubuntu>

```bash
wget -O - https://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest/SALTSTACK-GPG-KEY.pub | sudo apt-key add -
sudo touch /etc/apt/sources.list.d/saltstack.list

# add follwing
# deb http://repo.saltstack.com/apt/ubuntu/16.04/amd64/latest xenial main
vim /etc/apt/sources.list.d/saltstack.list

sudo apt-get install salt-master
sudo apt-get install salt-minion
sudo apt-get install salt-ssh
sudo apt-get install salt-syndic
sudo apt-get install salt-cloud
sudo apt-get install salt-api
sudo systemctl restart salt-minion
```
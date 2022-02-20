# setup ansible centos
Made 3 Centos 8 machines ready 
```sh
192.168.1.10
192.168.1.11
192.168.1.12
```
Use 192.168.1.10 as control machine, others for nodes

all of them has sonnyyu as sudo user .
```sh
su 
usermod -aG wheel sonnyyu
```

Install ansible at control machine (192.168.1.10):
```sh
sudo yum install epel-release -y
sudo yum install ansible -y
```
Create devops user at control machine
```sh
sudo userdel -r devops
sudo adduser devops
sudo passwd devops
sudo usermod -aG wheel devops
su devops
cd ~
ssh-keygen
```
Make sure current user as devops
```sh
$ whoami
devops
```
Clone github
```sh
git clone https://github.com/sonnyyu/setupansiblecentos
cd setupansiblecentos
```
Edit hosts-dev with IP address
```sh
nano hosts-dev
[webservers]
app1 ansible_host=192.168.1.11
app2 ansible_host=192.168.1.12
```
Install ansible.posix
```sh
ansible-galaxy collection install ansible.posix 
```
Run Playbook to create password less login at nodes
```sh
ansible-playbook playbook.yml -usonnyyu -bK --ask-pass
```
Test password less ssh login
```sh
ansible-playbook  checkpwless.yml
```
Test Ad-hoc 
```sh
ansible all -m ping
ansible all -a "df -h" 
ansible all -a "free -h"
ansible all -m yum -a "name=tree state=latest" -b
ansible all -a "uptime"
```


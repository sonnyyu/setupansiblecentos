# setup ansible ubuntu
Made 3 Ubuntu18.04 machines ready 
```sh
192.168.1.1
192.168.1.2
192.168.1.3
```
Use 192.168.1.1 as control machine, others for nodes

all of them has sonnyyu as sudo user .

Install ansible at control machine (192.168.1.1):
```sh
sudo apt-add-repository ppa:ansible/ansible -y
sudo apt update -y
sudo apt install ansible -y
```
Create devops user at control machine
```sh
sudo adduser devops
sudo usermod -aG sudo devops
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
git clone https://github.com/sonnyyu/setupansibleubuntu
cd setupansibleubuntu
```
Edit hosts-dev with IP address
```sh
[webservers]
app1 ansible_host=192.168.1.2
app2 ansible_host=192.168.1.3
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
ansible all -m apt -a "name=tree state=latest" -b
ansible all -a "uptime"
```


#  Setting Up Ansible
```
#!/bin/bash
sudo apt update -y
sudo apt-add-repository ppa:ansible/ansible 
sudo apt install ansible -y
ansible --version
```
[https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-20-04#step-1-installing-ansible]
# Create Roles
```
ansible-galaxy init --offline -f webrole

OR

ansible-galaxy init webrole
```
# Check Status
```
ansible-playbook  -i hosts mysql_playbook.yaml --check
```
# Deploy Service
```
ansible-playbook  -i hosts mysql_playbook.yaml 
```
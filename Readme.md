#  Setting Up Ansible
[]
```
sudo apt update
sudo apt-add-repository ppa:ansible/ansible
sudo apt install ansible
ansible --version
```
# Create Roles
```
ansible-galaxy init --offline -f webrole

OR

ansible-galaxy init webrole
```
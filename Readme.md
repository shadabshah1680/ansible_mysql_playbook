#  Setting Up Ansible

```
#!/bin/bash
source  /etc/os-release
if [[ "$ID_LIKE" == "debian" ]]; then
    echo "Detected APT package manager..."
    sudo apt update -y
    sudo apt-add-repository ppa:ansible/ansible
    sudo apt install ansible -y
elif [[ "$ID_LIKE" == "rhel fedora" || "$ID_LIKE" == "rhel" ]]; then
    echo "Detected YUM package manager..."
    sudo yum update -y
    sudo yum install epel-release -y
    sudo yum install ansible -y
elif [[ "$ID_LIKE" == "centos rhel fedora" ]]; then
    echo "Detected Amazon Linux package manager..."
    sudo yum update -y
    sudo amazon-linux-extras install epel -y
    sudo yum install ansible -y
else
echo "Unable to determine package manager. Exiting..."
exit 1
fi
```
- [centos| https://www.simplilearn.com/tutorials/ansible-tutorial/ansible-installation]
- [ubuntu| https://www.digitalocean.com/community/tutorials/how-to-install-and-configure-ansible-on-ubuntu-20-04#step-1-installing-ansible]
- In case ID_LIKE not working use `#ID_LIKE=$(cat /etc/os-release | grep ID_LIKE | cut -d"=" -f2) #hard_code`
#  Ansible client Nodes Prerequisite
> Need to setup ssh connection between ansible node and client nodes
- Generate key using `ssh-keygen` in ansible server
- put `id_rsa.pub` in client nodes authorized_keys
## Sample User Data Script
```
#!/bin/bash
for dir in /home/*; do
user=$(echo $dir | cut -d"/" -f3)
su $user -c "cat >>$dir/.ssh/authorized_keys<<EOF
ssh-rsa kw2e2adsasasashere user@unknown
EOF"
done
```
# Create Roles
```
mkdir roles && cd roles && ansible-galaxy init --offline -f mysql.role

OR

ansible-galaxy init mysql.role
```
# Setup hosts
- Set public_key of ansible server in authorized key of client nodes to make sure that ssh connection is authorized
- Change the ip in inventory file 
    - client-server-ip1
    - client-server-ip2
- You can add more ips  in a servers group and labels to categorized the number of servers group accordingly
# Check Status
```
ansible-playbook -i inventory  dev-playbook.yml  --check
```
# Deploy Service
```
ansible-playbook -i inventory  dev-playbook.yml
```
 
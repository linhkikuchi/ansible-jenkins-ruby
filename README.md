# ansible-jenkins-ruby
# Readme
This playbook is written following ansible 2.* syntax


Jenkins 2.x introduces an interactive Setup Wizard which breaks
automatic configuration.
If you want to disable the Setup Wizard, run the setting.yml.
Jenkins 2.x security options
- Prevent Cross Site Request Forgery exploits
- Use browser for metadata download

These options prevent installing plugins by jenkins-cli.
If you want to install plugins by jenkins-cli, pls run plugins.yml after 
- Disable Prevent Cross Site Request Forgery exploits
- Enable Use browser for metadata download

## Before running the playbook
- Create hosts file with Server IP inside
```
echo "[hosts]
$IP" >> hosts
```
- Copy keys to host IP
```
## copy key to new server
ssh-keyscan $IP >>  ~/.ssh/known_hosts
sshpass -p "$password" ssh-copy-id -i ~/.ssh/id_rsa root@$IP
```

## Description
To install jenkins
jenkins.yml is to install java, git, jenkins, ansible, set up ntp to sync the clock
```
ansible-playbook jenkins.yml -i hosts -u root
```
To install rbenv and ruby for ruby team
```
ansible-playbook rbenv.yml -i hosts -u root
ansible-playbook ruby.yml -i hosts -u root
```

## nova launch VM 
In order to use os_server (openstack) in ansible, we have to install
- python
- python-devel
- ansible
- shade
- python openstack client
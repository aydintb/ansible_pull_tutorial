sudo crontab -u ansible -e
cat /var/log/syslog | grep CRON


ssh-keygen -t ed25519 -C "this is a comment"
ssh-copy-id -i ~/.ssh/id_ed25519.pub 172.16.250.132
ssh 172.16.250.132

ssh-keygen -t ed25519 -C "ansible"
     use a different name  /home/atb/.ssh/ansible
   (do not use a passphrase)


ssh-copy-id -i ~/.ssh/ansible.pub 192.168.116.128


#sudo nano /etc/ansible/hosts
localhost ansible_connection=local


to run this ansible:

/usr/bin/ansible-pull -U https://github.com/aydintb/ansible_pull_tutorial.git



ansible all --key-file ~/.ssh/ansible -i -m ping


# after creating ansible.cfg:
ansible all -m ping

ansible all -m gather_facts

ansible all -m gather_facts --limit 192.168.116.128

ansible all -m apt -a update_cache=true --become --ask-become-pass

---------------- encrpt files -------------

ansible-vault encrypt --vault-password-file ~/.vault_key sudoers_ansible

this will fail:

/usr/bin/ansible-pull -U https://github.com/aydintb/ansible_pull_tutorial.git


# copy the key to the server, so it can decrypt

scp /home/atb/.vault_key 172.16.250.133:


/usr/bin/ansible-pull --vault-password-file ~/.vault_key -U https://github.com/aydintb/ansible_pull_tutorial.git



------------------

bir ust folder'da github'a aktarilmayacak sekilde
.vault_key file icinde password olacak.
chmod 600 ~/.vault_key
# now only the owner has access to this file, noone else can read or write


#random text file to encrypt
nano info.txt

ansible-vault encrypt info.txt

New Vault password:
Confirm New Vault password:

ansible-vault decrypt --vault-password-file ~/.vault_key info.txt

Decryption successful

atb@u20043:~/ansible_pull_tutorial$ cat info.txt


ansible-vault edit --vault-password-file ~/.vault_key info.txt

ansible-vault view --vault-password-file ~/.vault_key info.txt


---------------------------------------------


- hosts: host2
  tasks:
    - shell: echo "hello world 2"


commands similar to the "update_cache" are listed in the web page:
https://docs.ansible.com/ansible/latest/collections/ansible/builtin/apt_module.html

install a package to all our servers with one command:

ansible all -m apt -a name=vim-nox --become --ask-become-pass

lastes version of snapd:

ansible all -m apt -a "name=snapd state=latest" --become --ask-become-pass


update all upgrades:

ansible all -m apt -a "upgrade=dist" --become --ask-become-pass


install apache:

ansible-playbook --ask-become-pass install_apache.yml

ansible-playbook --ask-become-pass remove_apache.yml


ansible all -m gather_facts --limit 192.168.116.128 | grep ansible_distribution

#if we need to add firewall on CentOS

sudo firewall-cmd --add-port=80/tcp

ansible-playbook --ask-become-pass site.yml

list used tags:

ansible-playbook --list-tags site.yml



use yml with tags:

ansible-playbook --tags apache --ask-become-pass site.yml

ansible-playbook --tags centos --ask-become-pass site.yml

ansible-playbook --tags "apache,db" --ask-become-pass site.yml


managing files:


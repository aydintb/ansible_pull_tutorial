
ssh-keygen -t ed25519 -C "this is a comment"
ssh-copy-id -i ~/.ssh/id_ed25519.pub 172.16.250.132
ssh 172.16.250.132

ssh-keygen -t ed25519 -C "ansible"
     use a different name  /home/atb/.ssh/ansible
   (do not use a passphrase)


ssh-copy-id -i ~/.ssh/ansible.pub 192.168.116.128


to run this ansible:

/usr/bin/ansible-pull -U https://github.com/aydintb/ansible_pull_tutorial.git



ansible all --key-file ~/.ssh/ansible -i -m ping


# after creating ansible.cfg:
ansible all -m ping

ansible all -m gather_facts
ansible all -m gather_facts --limit 192.168.116.128

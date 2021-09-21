to run this ansible:

/usr/bin/ansible-pull -U https://github.com/aydintb/ansible_pull_tutorial.git


 ansible all --key-file ~/.ssh/ansible -i -m ping
 # ping creates connection, not a tcp ping.

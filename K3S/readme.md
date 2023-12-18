## Installation of the K3S

### Introduction
You may find information on K3S here https://docs.k3s.io/related-projects

This installation relies on Ansible to automate the boring stuff, Make sure you have Ansible installed in your Mac. (if not, "brew install ansible")
Ansible will also help us in case one make a mess and need to start over <(^_^)>

### Getting Ansible playbook
- goto to https://github.com/k3s-io/k3s-ansible
- click on CODE and download ZIP

  k3s_cluster:
  children:
    server:
      hosts:
        turingRP-master.local:
    agent:
      hosts:
        turingRP-worker-1.local:
        turingRP-worker-2.local:

  Required Vars
  vars:
    ansible_port: 22
    ansible_user: rp

ansible-playbook playbook/site.yml -i inventory.yml


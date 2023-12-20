## Installation of the K3S

### Introduction

You may find information on K3S here https://docs.k3s.io/related-projects

This installation relies on Ansible to automate the boring stuff, Make sure you have Ansible installed in your Mac. (if not, "brew install ansible")
Ansible will also help us in case one make a mess and need to start over <(^\_^)>

### Preparing the RaspberryCM4 OS

- We need to turn off swap:

  - ssh into CM4
  - verify if swap is enabled
    - cat /proc/meminfo | grep SwapTotal
    - if the response shows SwapTotal different than '0 kB', it is enabled
  - to permanently disable it as required by K3S
    - sudo nano /etc/dphys-swapfile
    - set `CONF_SWAPSIZE = 0`
    - save file
  - sudo reboot now

- to certify that swap is disabled

  - ssh again into same CM4
  - cat /proc/meminfo | grep SwapTotal
  - the response should show `SwapTotal: 0 kB`

- repeat for each CM4

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

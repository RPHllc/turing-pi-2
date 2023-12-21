## Installation of the K3S

### Introduction

You may find information on K3S here https://docs.k3s.io/related-projects

[ NOT AUTOMATED YET, THE STEPS BELOW ARE MANUAL FOR NOW:
This installation relies on Ansible to automate the boring stuff, Make sure you have Ansible installed in your Mac. (if not, "brew install ansible")

Ansible will also help us in case one make a mess and need to start over <(^\_^)>
]

### Preparing the RaspberryCM4 OS

- ssh into CM4
- turn off swap:
  - sudo nano /etc/dphys-swapfile
  - set `CONF_SWAPSIZE = 0`
  - save file
- configure cgroup:

  - sudo nano /boot/cmdline.txt
    - this file has a single line, do not delete it
    - add at the end of the line:
      ```
       cgroup_enable=cpuset cgroup_memory=1 cgroup_enable=memory
      ```
  - save file

- sudo reboot now

- repeat for each CM4

- to certify that swap is disabled
  - ssh into each CM4
  - cat /proc/meminfo | grep SwapTotal
  - the response should show `SwapTotal: 0 kB`

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

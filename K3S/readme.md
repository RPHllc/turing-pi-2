## Installation of the K3S

### Introduction

You may find information on K3S here https://docs.k3s.io/related-projects

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

- to certify that swap is disabled (optional)
  - ssh into each CM4
  - cat /proc/meminfo | grep SwapTotal
  - the response should show `SwapTotal: 0 kB`

### Installing K3S

- Master node

  - ssh to your master node
  - `sudo su`
  - `curl -sfL https://get.k3s.io | sh -`
  - wait for the prompt and get a token using
  - `cat /var/lib/rancher/k3s/server/node-token`
  - this token will be used to set the worker nodes
  - type `exit` to leave the superuser mode

- Worker node (repeat for each worker)

  - ssh to your worker node
  - `sudo su`
  - `curl -sfL https://get.k3s.io | K3S_URL=https://<master-node-IP>:6443 K3S_TOKEN=<token> sh -`
  - wait for the prompt
  - type `exit` to leave the superuser mode

- Verify
  - ssh to your master node
  - type `sudo kubectl get nodes`
  - you should see the 3 nodes, the roles of the master are control-plane, master and the roles for the workers are "none"

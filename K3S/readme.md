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

      `cgroup_enable=cpuset cgroup_memory=1  group_enable=memory`

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

### Touch up to enable seamless use of kubectl

We will set kubectl to be used from a terminal opened in user machine (Mac) and without need to ssh any node. kubectl will also be accessible at the master node using sudo.

- Prepare your Mac

  - On a terminal:
  - `brew install kubectl`
  - `mkdir ~/.kube`
  - `touch ~/.kube/config`

- ssh to your master node

  - permanently set path to config

    `sudo nano /etc/environment`

  - add the line below (or replace an existing line with KUBECONFIG)

    `KUBECONFIG=/etc/rancher/k3s/k3s.yaml`

  - save file and exit nano
  - `sudo cat /etc/rancher/k3s/k3s.yaml`
  - copy the content of this file
  - reboot master node

    `sudo reboot now`

- on the mac terminal
  - nano ~/.kube/config
  - paste the content of the file (from the master node)
  - change the IP address by the IP address of the master node
  - save file

### Test everything!!

- on a terminal on the Mac type

  `kubectl get nodes`
  The list of the three nodes should be available

- ssh to master node and type

  `sudo kubectl get nodes`
  or

  `sudo su -`
  `kubectl get nodes`

  The list of the three nodes should be available

### You are done and your K3S clusters are running!

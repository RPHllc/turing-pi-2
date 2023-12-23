## Longhorn installation

### Introduction

The objective of installing Longhorn is to provide persistant volumes to the pods running on the Kubernet (K3S) cluster. Longhorn abstracts the hardware location from each pods and supports data sharing between pod replicas.

### Prepare the CM4 operating system

On each node, install the following:

`sudo apt -y install nfs-common open-iscsi util-linux`

Format the disk

`mkfs.ext4 /dev/sda`

Create data folder

`mkdir /mnt/ssd`

Add line to /etc/fstab to auto mount this disk to /ssd on boot

`echo "/dev/sda /mnt/ssd ext4 defaults 0 0" | tee -a /etc/fstab`

Mount the disk to /mnt/ssd folder

`mount -a`

Confirm the /mnt/ssd is mounted with

`df -h /mnt/ssd`

Above should return something similar to this:

Filesystem Size Used Avail Use% Mounted on  
/dev/sda 458G 28K 435G 1% /mnt/ssd

Create directory that Longhorn will use

`mkdir /mnt/ssd/longhorn`

### Installation

Open a terminal in your mac and run

`kubectl apply -f https://raw.githubusercontent.com/longhorn/longhorn/v1.5.3/deploy/longhorn.yaml`

The installation takes time, you can monitor progress with

`kubectl get pods --namespace longhorn-system --watch`

When the screen stops changing ctrl-C and

`kubectl -n longhorn-system get pod`

If there are several pods on the longhorn-system namespace, it is running!!!

### Accessing the Longhorn UI

- get Longhorn's external IP

  `kubectl -n longhorn-system get svc`

- lookfor longhorn-frontend cluster-ip

- create an Ingress with basic authentication (nginx)

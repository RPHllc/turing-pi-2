## Stopping K3S

To shutdown the cluster, particularly if you are using persistant volumes (e.g. from Longhorn), you should use

`/usr/local/bin/k3s-killall.sh`

from a master node.

The k3s-killall.sh script stops all of the K3s containers and reset the containerd state. It cleans up containers, K3s directories, and networking components while also removing the iptables chain with all the associated rules. The cluster data will not be deleted.

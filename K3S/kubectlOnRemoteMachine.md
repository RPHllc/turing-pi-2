Running kubectl on a remote machine, such as a laptop or desktop has many benefits. For example, one can monitor a kubernets cluster without having to ssh in any node.

To run `kubectl` on a remote machine to manage a Kubernetes cluster, follow these steps:

1. **Install `kubectl`**: Ensure `kubectl` is installed on your local machine [[4](https://dzone.com/articles/setting-up-kubernetes-k8s-on-windows)]. Use the appropriate installation method for your operating system.

2. **Copy Configurations**: Obtain the Kubernetes configuration file (`kubeconfig`) from the remote machine. Copy it to your local machine. This file typically includes cluster details, authentication information, and context settings [[2](https://dev.to/gvelrajan/configure-local-kubectl-to-remote-access-kubernetes-cluster-2g81)].

``` bash
   scp 10.0.154.241:/etc/rancher/k3s/k3s.yaml ~/.kube/config
```

4. **Set `KUBECONFIG` Environment Variable**: Set the `KUBECONFIG` environment variable on your local machine to point to the copied configuration file. This allows `kubectl` to use the correct configuration when interacting with the remote cluster [[3](https://medium.com/@rajkumar.rajaratnam/configure-local-kubectl-to-access-remote-kubernetes-cluster-ee78feff2d6d)].

5. **Verify Connectivity**: Test connectivity by running `kubectl get pods` or similar commands. Ensure `kubectl` correctly uses the remote cluster configuration [[1](https://stackoverflow.com/questions/36306904/configure-kubectl-command-to-access-remote-kubernetes-cluster-on-azure)].

By following these steps, you can effectively manage a remote Kubernetes cluster using `kubectl` from your local machine.

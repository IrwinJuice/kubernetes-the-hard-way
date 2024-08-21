# Set Up The Jumpbox

In this lab you will set up one of the four machines to be a `jumpbox`. This machine will be used to run commands in this tutorial. While a dedicated machine is being used to ensure consistency, these commands can also be run from just about any machine including your personal workstation running macOS or Linux.

Think of the `jumpbox` as the administration machine that you will use as a home base when setting up your Kubernetes cluster from the ground up. One thing we need to do before we get started is install a few command line utilities and clone the Kubernetes The Hard Way git repository, which contains some additional configuration files that will be used to configure various Kubernetes components throughout this tutorial. 

Log in to the `jumpbox` with user:

```bash
ssh IJ@jumpbox
```
### Install Command Line Utilities

Now that you are logged into the `jumpbox` machine as the `root` user, you will install the command line utilities that will be used to preform various tasks throughout the tutorial. 

```bash
yum -y install wget curl neovim openssl git
```

### Sync GitHub Repository

Now it's time to download a copy of this tutorial which contains the configuration files and templates that will be used build your Kubernetes cluster from the ground up. Clone the Kubernetes The Hard Way git repository using the `git` command:

```bash
git clone https://github.com/IrwinJuice/kubernetes-the-hard-way.git
```

```bash
git switch -c oracle-amd64 origin/oracle-amd64
```

Change into the `kubernetes-the-hard-way` directory:

```bash
cd kubernetes-the-hard-way
```

This will be the working directory for the rest of the tutorial. If you ever get lost run the `pwd` command to verify you are in the right directory when running commands on the `jumpbox`:

```bash
pwd
```

```text
/home/IJ/kubernetes-the-hard-way
```

### Download Binaries

In this section you will download the binaries for the various Kubernetes components. The binaries will be stored in the `downloads` directory on the `jumpbox`, which will reduce the amount of internet bandwidth required to complete this tutorial as we avoid downloading the binaries multiple times for each machine in our Kubernetes cluster.

From the `kubernetes-the-hard-way` directory create a `downloads` directory using the `mkdir` command:

```bash
mkdir downloads
```

The binaries that will be downloaded are listed in the `downloads.txt` file, which you can review using the `cat` command:

```bash
cat downloads.txt
```

Download the binaries listed in the `downloads.txt` file using the `wget` command:

```bash
wget -q --show-progress \
  --https-only \
  --timestamping \
  -P downloads \
  -i downloads.txt
```

Depending on your internet connection speed it may take a while to download the `584` megabytes of binaries, and once the download is complete, you can list them using the `ls` command:

```bash
ls -loh downloads
```

```text
total 584M
-rw-r--r--. 1 IJ  41M May  9  2023 cni-plugins-linux-arm64-v1.3.0.tgz
-rw-r--r--. 1 IJ  34M Oct 27  2023 containerd-1.7.8-linux-arm64.tar.gz
-rw-r--r--. 1 IJ  22M Aug 14  2023 crictl-v1.28.0-linux-arm.tar.gz
-rw-r--r--. 1 IJ  15M Jul 11  2023 etcd-v3.4.27-linux-arm64.tar.gz
-rw-r--r--. 1 IJ 111M Oct 18  2023 kube-apiserver
-rw-r--r--. 1 IJ 107M Oct 18  2023 kube-controller-manager
-rw-r--r--. 1 IJ  46M Oct 18  2023 kubectl
-rw-r--r--. 1 IJ 101M Oct 18  2023 kubelet
-rw-r--r--. 1 IJ  51M Oct 18  2023 kube-proxy
-rw-r--r--. 1 IJ  52M Oct 18  2023 kube-scheduler
-rw-r--r--. 1 IJ 9.6M Aug 11  2023 runc.arm64

```

### Install kubectl

In this section you will install the `kubectl`, the official Kubernetes client command line tool, on the `jumpbox` machine. `kubectl will be used to interact with the Kubernetes control once your cluster is provisioned later in this tutorial.

Use the `chmod` command to make the `kubectl` binary executable and move it to the `/usr/local/bin/` directory:

```bash
{
  chmod +x downloads/kubectl
  sudo cp downloads/kubectl /usr/local/bin/kubectl
}
```

At this point `kubectl` is installed and can be verified by running the `kubectl` command:

```bash
kubectl version --client
```

```text
Client Version: v1.28.3
Kustomize Version: v5.0.4-0.20230601165947-6ce0bf390ce3
```

At this point the `jumpbox` has been set up with all the command line tools and utilities necessary to complete the labs in this tutorial.

Next: [Provisioning Compute Resources](03-compute-resources.md)

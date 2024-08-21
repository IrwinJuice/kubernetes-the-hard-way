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
total 557M
-rw-r--r--. 1 IJ 46M Jun 17 18:51 cni-plugins-linux-amd64-v1.5.1.tgz
-rw-r--r--. 1 IJ 46M Jul 18 07:19 containerd-1.7.20-linux-amd64.tar.gz
-rw-r--r--. 1 IJ 18M Aug 13 13:48 crictl-v1.31.1-darwin-amd64.tar.gz
-rw-r--r--. 1 IJ 21M Jul 19 23:36 etcd-v3.5.15-darwin-amd64.zip
-rw-r--r--. 1 IJ 87M Aug 13 17:23 kube-apiserver
-rw-r--r--. 1 IJ 81M Aug 13 17:23 kube-controller-manager
-rwxr-xr-x. 1 IJ 54M Aug 13 17:23 kubectl
-rw-r--r--. 1 IJ 74M Aug 13 17:23 kubelet
-rw-r--r--. 1 IJ 62M Aug 13 17:23 kube-proxy
-rw-r--r--. 1 IJ 61M Aug 13 17:23 kube-scheduler
-rw-r--r--. 1 IJ 11M Jun 13 19:12 runc.amd64
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
Client Version: v1.31.0
Kustomize Version: v5.4.2
```

At this point the `jumpbox` has been set up with all the command line tools and utilities necessary to complete the labs in this tutorial.

Next: [Provisioning Compute Resources](03-compute-resources.md)

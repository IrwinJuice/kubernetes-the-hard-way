# Prerequisites

In this lab you will review the machine requirements necessary to follow this tutorial.

## Virtual or Physical Machines

This tutorial requires four (4) virtual or physical AMD64 machines running Oracle 9.4. The follow table list the four machines and thier CPU, memory, and storage requirements.

| Name    | Description            | CPU | RAM   | Storage |
|---------|------------------------|-----|-------|---------|
| jumpbox | Administration host    | 1   | 512MB | 10GB    |
| server  | Kubernetes server      | 1   | 2GB   | 20GB    |
| node-0  | Kubernetes worker node | 1   | 2GB   | 20GB    |
| node-1  | Kubernetes worker node | 1   | 2GB   | 20GB    |
## Virtual Box
![vm.png](..%2Fvm.png)
## Oracle Linux

### add user in `sudoers`

-   `su root`
- `usermod -aG root IJ`
- `usermod -aG wheel IJ`
- `vi /etc/sudoers`

**after** `root     ALL=(ALL) ALL` **add**

`username ALL=(ALL) ALL`

Next: [setting-up-the-jumpbox](02-jumpbox.md)

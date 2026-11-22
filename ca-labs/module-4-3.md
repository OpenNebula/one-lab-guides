---
layout: default
title: Lab 3 - Custom Probes
parent: Module 4 - Hosts
---
# Module 4 - Lab 2: Custom Probes
{: .no_toc}

## Table of Contents
{: .no_toc}

<details markdown="block">
  <summary>
    Expand to access the In-page navigation
  </summary>
  {: .text-delta }
1. TOC
{:toc}
</details>

## Objective(-s):

- Locate and Inspect Built-in Probes.
- Create a Custom Probe.

# Locate and Inspect Built-in Probes.

## 4.2.1

As **oneadmin** ssh to Node 2 from Node 1.

```console
ssh lab-X-node2
```

Inspect the probes directory.

```console
ls -lh /var/tmp/one/im/qemu-probes.d/
```

```console
total 8.0K
drwxr-x--- 5 oneadmin oneadmin 4.0K Aug 16 08:32 host
drwxr-x--- 5 oneadmin oneadmin 4.0K Aug 16 08:32 vm
```

## 4.2.2

Using your preferred text viewer - inspect one of the probes under **host** directory:

```console
cat /var/tmp/one/im/qemu-probes.d/host/system/cpu.sh
```

Now try to run this probe manually

```console
/var/tmp/one/im/qemu-probes.d/host/system/cpu.sh
```

```console
MODELNAME="Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz"
```

# Create a Custom Probe.

## 4.2.3

Go back to Node 1's Command Line and make sure you are logeed in as **oneadmin**.

Clone the repository.

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set Probes
git checkout
cd Probes
ls -lh
```

```console
total 4.0K
-rw-rw-r-- 1 oneadmin oneadmin 133 Aug 19 10:29 host_mode.py
```

Copy the **host_mode.py** script to the Probes directory and make it executable!

```console
cp host_mode.py ~/remotes/im/qemu-probes.d/host/system/host_mode.py
chmod +x ~/remotes/im/qemu-probes.d/host/system/host_mode.py
```
## 4.2.4

Execute the **sync** command.

```console
onehost sync --force
```

Wait until all hosts are in sync. 

```console
* Adding lab-2022-node3 to upgrade
* Adding lab-2022-node2 to upgrade
* Adding 3.74.228.185 to upgrade
* Adding 3.71.32.116 to upgrade
[========================================] 4/4 3.71.32.116
All hosts updated successfully.
```

## 4.2.5

{: .note}
> It may take from 3 to 5 minutes to gather this metric. Feel free to proceed with the [Module 4 - Lab 4](/one-lab-guides/ca-labs/module-4-4.html) and return to this later.

Run onehost show command on one of the hosts and check the **Monitoring** section and look for **MODE** parameter. It should show either PROD,TEST or DEV.

```console
onehost show 2
```

```console
Node 2 INFORMATION                                                              
ID                    : 2                   
NAME                  : lab-X-node2       
CLUSTER               : default             
STATE                 : MONITORED           
IM_MAD                : qemu                
VM_MAD                : qemu                
LAST MONITORING TIME  : 08/16 16:13:38      
...
MONITORING INFORMATION
...
MODE="PROD"
MODELNAME="Intel(R) Xeon(R) CPU E5-2686 v4 @ 2.30GHz"
RESERVED_CPU=""
...
```

# Congratulations, you've completed the assignment!
{: .no_toc}
---
layout: default
title: Lab 1 - Enable VM HA
parent: Module 7 - Hooks
---
# Module 7 - Lab 1 : Enable VM HA
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
- Create a System DS with the Shared Driver
- Create an Image DS with the Shared Driver
- Mount shares across the environment
- Deploy a VM
- Configure VM HA
- Test VM HA

# Create System DS with the Shared Driver

## 7.1.1

Navigate to **Storage -> Datastores**.

<img src="./../assets/ce-images/module7_lab1/s1.png">

## 7.1.2

Press **Create Datastore**.

<img src="./../assets/ce-images/module7_lab1/s2.png">

## 7.1.3

Make sure to set the **Type** to **SYSTEM**.

Give it a name. 

Select the **Filesystem - shared mode** for the **Storage backend**.

<img src="./../assets/ce-images/module7_lab1/s3.png">

## 7.1.4

Set the cluster to **default**.

<img src="./../assets/ce-images/module7_lab1/s4.png">

## 7.1.5

Keep the **Configuration attributes** settings as is.

<img src="./../assets/ce-images/module7_lab1/s5.png">

## 7.1.6

Keep the **Custom Variables** settings as is and press the **Finish** button.

<img src="./../assets/ce-images/module7_lab1/s6.png">

# Create an Image DS with the Shared Driver

## 7.1.7

Press **Create Datastore**.

<img src="./../assets/ce-images/module7_lab1/s7.png">

## 7.1.8

Make sure to set the **Type** to **IMAGE**.

Give it a name. 

Select the **Filesystem - shared mode** for the **Storage backend**.

<img src="./../assets/ce-images/module7_lab1/s8.png">

## 7.1.9

Set the cluster to **default**.

<img src="./../assets/ce-images/module7_lab1/s9.png">

## 7.1.10

Set the shared **SYSTEM** datastore as the only **Compatible system datastore**.

<img src="./../assets/ce-images/module7_lab1/s10.png">

## 7.1.11

Keep **Custom Variables** as is and press the **Finish** button.

<img src="./../assets/ce-images/module7_lab1/s11.png">

## 7.1.12

You should end up having two shared datastores with IDs 100 & 101.

<img src="./../assets/ce-images/module7_lab1/s12.png">

# Mount shares across the environment

{: .note }
> In this lab environment the Frontend Node is acting as the NFS server! While it is suitable for the test envs, please avoid replicating this in production.

## 7.1.13

Connect to the Frontend Node first and make sure you are root. 

```console
ssh ubuntu@<FE IP>
sudo su
```

Open the **fstab** file in a preferred editor.

```console
vi /etc/fstab
```

Append the following lines.

```console
<FE IP>:/system /var/lib/one/datastores/100 nfs4 defaults,_netdev,nfsvers=4.2 0 0
<FE IP>:/images /var/lib/one/datastores/101 nfs4 defaults,_netdev,nfsvers=4.2 0 0
```

Save the file.

## 7.1.14

Execute the verify command

```console
findmnt --verify
```

Make sure you have no errors in the output

```console
Success, no errors or warnings detected
```

Reload the systemctl daemon and execute mount command to mount NFS shares.

```console
systemctl daemon-reload
mount -a
```

## 7.1.15

From the VDI connect to the Hypervisor Node.

```console
ssh ubuntu@<KVM 1>
sudo su
```

Open the **fstab** file in a preferred editor.

```console
vi /etc/fstab
```

Append the following lines.

```console
<FE IP>:/system /var/lib/one/datastores/100 nfs4 defaults,_netdev,nfsvers=4.2 0 0
<FE IP>:/images /var/lib/one/datastores/101 nfs4 defaults,_netdev,nfsvers=4.2 0 0
```

Create two directories for these shares.

```console
sudo -iu oneadmin mkdir /var/lib/one/datastores/100
sudo -iu oneadmin mkdir /var/lib/one/datastores/101
```

## 7.1.16

Execute the verify command

```console
findmnt --verify
```

Make sure you have no errors in the output

```console
Success, no errors or warnings detected
```

Reload the systemctl daemon and execute mount command to mount NFS shares.

```console
systemctl daemon-reload
mount -a
```
  
## 7.1.17

From the VDI connect to the other Hypervisor Node.

```console
ssh ubuntu@<KVM 1>
sudo su
```

Open the **fstab** file in a preferred editor.

```console
vi /etc/fstab
```

Append the following lines.

```console
<FE IP>:/system /var/lib/one/datastores/100 nfs4 defaults,_netdev,nfsvers=4.2 0 0
<FE IP>:/images /var/lib/one/datastores/101 nfs4 defaults,_netdev,nfsvers=4.2 0 0
```

Create two directories for these shares.

```console
sudo -iu oneadmin mkdir /var/lib/one/datastores/100
sudo -iu oneadmin mkdir /var/lib/one/datastores/101
```

## 7.1.18

Execute the verify command

```console
findmnt --verify
```

Make sure you have no errors in the output

```console
Success, no errors or warnings detected
```

Reload the systemctl daemon and execute mount command to mount NFS shares.

```console
systemctl daemon-reload
mount -a
```

# Deploy a VM

## 7.1.19

Navigate to **Datastores -> Images**.

<img src="./../assets/ce-images/module7_lab1/s19.png">

## 7.1.20

Locate the **Service FlaskApp** image and press the **Clone** button.

<img src="./../assets/ce-images/module7_lab1/s20.png">

## 7.1.21

Name it differently from the original Image.

<img src="./../assets/ce-images/module7_lab1/s21.png">

## 7.1.22

Select the **shared** datastore and press the **Finish** button.

<img src="./../assets/ce-images/module7_lab1/s22.png">

## 7.1.23

Wait until the Image is in the **Ready** state.

<img src="./../assets/ce-images/module7_lab1/s23.png">

## 7.1.24

Go to **Instances -> VMs**

<img src="./../assets/ce-images/module7_lab1/s24.png">

## 7.1.25

Press **Create VM**.

<img src="./../assets/ce-images/module7_lab1/s25.png">

## 7.1.26

From the list select the **Service FlaskApp** VM Template.

<img src="./../assets/ce-images/module7_lab1/s26.png">

## 7.1.27

Leave the **Configuration** as is and proceed to the next screen.

<img src="./../assets/ce-images/module7_lab1/s27.png">

## 7.1.28

Set the password and proceed to the **Advanced options**.

<img src="./../assets/ce-images/module7_lab1/s28.png">

## 7.1.29

Under the **Disks** section locate the one with ID 0 and select the **Edit** option from the three-dot menu.

<img src="./../assets/ce-images/module7_lab1/s29.png">

## 7.1.30

Select the clone of a Service FlaskApp and press **Save**.

<img src="./../assets/ce-images/module7_lab1/s30.png">

## 7.1.31

Press Finish and wait until the VM is in the running state.

<img src="./../assets/ce-images/module7_lab1/s31.png">

# Configure VM HA

{: .note }
> In this lab we will set the monitoring settings to be quite aggressive.

## 7.1.32

As root open the **monitord.conf** file in a preferred text editor.

```console
sudo su
vi /etc/one/monitord.conf
```

Locate and set the following variables to the values as seen below.

```console
MANAGER_TIMER = 5
MONITORING_INTERVAL_HOST = 15
```

Then locate the next set of variables and set to the values as seen below.

```console
PROBES_PERIOD = [
    BEACON_HOST    = 2,
    ...
]
```

Save the changes and restart the opennebula daemon.

```console
systemctl restart opennebula
```

## 7.1.33

As **oneadmin** create the file.

```console
vi hook.cfg
```

And paste the following contents

{: .warning }
> Please note that in this lab we are using the --no-fencing option. While it's safe in the lab environment - you must avoid running this in a production. Fencing is the important mechanism that prevents split-brain issues.

```console
ARGUMENTS       = "$TEMPLATE -m -p 0 --no-fencing"
ARGUMENTS_STDIN = "yes"
COMMAND         = "ft/host_error.rb"
NAME            = "host_error"
STATE           = "ERROR"
REMOTE          = "no"
RESOURCE        = HOST
TYPE            = state
```

Create the hook using the **onehook** command line.

```console
onehook create hook.cfg
```

You shuld receive the ID of a hook as an output.

```console
ID: 0
```

# Test VM HA

## 7.1.34

Switch to the browser and extract the IP address of a FlaskApp VM.

<img src="./../assets/ce-images/module7_lab1/s34.png">

## 7.1.35

In the browser navigate to the extracted IP with port 5000 and press **Create the Travel Log**.

<img src="./../assets/ce-images/module7_lab1/s35.png">

## 7.1.36

Press **Return to Helm**.

<img src="./../assets/ce-images/module7_lab1/s36.png">

## 7.1.37

Press **Log the Travel**.

<img src="./../assets/ce-images/module7_lab1/s37.png">

## 7.1.38

Press **Log Another Travel** a few times.

<img src="./../assets/ce-images/module7_lab1/s38.png">

## 7.1.39

Press **Return to Helm**.

<img src="./../assets/ce-images/module7_lab1/s39.png">

## 7.1.40

Back in Sunstone identify the hypervisor that is hosting the VM.

<img src="./../assets/ce-images/module7_lab1/s40.png">

## 7.1.41

Connect to the host using SSH.

```console
ssh ubuntu@<KVM IP>
```

Execute the **reboot** command

```console
reboot
```

You must be notified that the server is about to be rebooted followed by the closed connection.

```console
The system will reboot now!

Connection to 62.210.249.11 closed by remote host.
Connection to 62.210.249.11 closed.
```

## 7.1.42

In Sunstone refresh the page and verify that the VM is running on a different host now!

<img src="./../assets/ce-images/module7_lab1/s42.png">

## 7.1.43

Switch to the Test App tab and press the **Read the Travel Log** button.

<img src="./../assets/ce-images/module7_lab1/s43.png">

## 7.1.44

Your database should exist and return the data. This proves that the VM wasn't recreated from scratch and that the data remained safe.

<img src="./../assets/ce-images/module7_lab1/s44.png">

# Terminate the VM in the preferred way!

    
# Congratulations, you've completed the assignment!
{: .no_toc}

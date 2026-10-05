---
layout: default
title: Lab 1 - Install and Configure OneKS
parent: Module 6 - OneKS
---
# Module 6 - Lab 1 : Install and Configure OneKS
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
- Install OneKS.
- Configure and start the service.
- Run the readiness check.

# Install the OneKS.

{: .warning }
> The commands in the guide should be executed as root
     
## 6.1.1

While connected to the Frontend Node - install the OneKS package.

```console
apt install opennebula-ks -y
```

# Configure and start the service.

## 6.1.2

Firslty configure the tproxy by editing the **OpenNebulaNetwork.conf** file. 

```console
vi /var/lib/one/remotes/etc/vnm/OpenNebulaNetwork.conf
```

Append the following.

```console
:tproxy:
  - :remote_addr: <FE IP>
    :remote_port: 5030
    :service_port: 5030
  - :remote_addr: <FE IP>
    :remote_port: 2633
    :service_port: 2633
```

Don't forget to save the file correctly.

## 6.1.3

Open the oned.conf file.

```console
vi /etc/one/oned.conf
```

Locate the **ONEGATE_ENDPOINT** and change it from your FE IP, to the tproxy's IP.

```console
ONEGATE_ENDPOINT = "http://169.254.16.9:5030"
```

## 6.1.4

Synchronise the configuration across all hosts.

```console
sudo -iu oneadmin onehost sync -f
```

Wait until all hosts are in sync.

```console
* Adding 62.210.249.11 to upgrade
* Adding 62.210.248.191 to upgrade
[========================================] 2/2 62.210.248.191 
```

## 6.1.5

Restart the OpenNebula daemon.

```console
systemctl restart opennebula
```

Restart the OneKS daemon.

```console
systemctl restart opennebula-ks
```

## 6.1.6

Verify whether OneKS is running.

```console
systemctl status opennebula-ks
```

Your output must look similar to the one below. 

```console
 opennebula-ks.service - OpenNebula Kubernetes Service
     Loaded: loaded (/usr/lib/systemd/system/opennebula-ks.service; disabled; preset: enabled)
     Active: active (running) since Mon 2026-09-14 10:39:14 UTC; 2s ago
   Main PID: 116930 (ruby)
      Tasks: 15 (limit: 19094)
     Memory: 62.1M (peak: 62.3M)
        CPU: 859ms
     CGroup: /system.slice/opennebula-ks.service
             └─116930 "puma 8.0.2 (tcp://127.0.0.1:10780) [/]"

Sep 14 10:39:15 f1 opennebula-ks[116930]: == Sinatra (v4.2.1) has taken the stage on 10780 for production with backup from Puma
Sep 14 10:39:15 f1 opennebula-ks[116930]: Puma starting in single mode...
Sep 14 10:39:15 f1 opennebula-ks[116930]: * Puma version: 8.0.2 ("Into the Arena")
Sep 14 10:39:15 f1 opennebula-ks[116930]: * Ruby version: ruby 3.2.3 (2024-01-18 revision 52bb2ac0a6) [x86_64-linux-gnu]
Sep 14 10:39:15 f1 opennebula-ks[116930]: *  Min threads: 0
Sep 14 10:39:15 f1 opennebula-ks[116930]: *  Max threads: 5
Sep 14 10:39:15 f1 opennebula-ks[116930]: *  Environment: production
Sep 14 10:39:15 f1 opennebula-ks[116930]: *          PID: 116930
Sep 14 10:39:15 f1 opennebula-ks[116930]: * Listening on http://127.0.0.1:10780
Sep 14 10:39:15 f1 opennebula-ks[116930]: Use Ctrl-C to stop
```

{: .warning }
> If your service is showing as (code=exited, status=1/FAILURE) then you should debug the OpenNebula Kubernetes Service before proceeding!

# Run the readiness check.

## 6.1.7

Run the **check** command and map the variables to the correct one.

Set the cluster to default (ID: 0).

Set the **Public network** to the ID of a **routable** network.

Set the **Private network** to the ID of a **private** network.

```console
oneks check
> OpenNebula cluster ID: 0
> Public network ID: 0
> Private network ID: 1
```

Your output must be simillar to the one below.

```console
---
[OK] Starting OneKS readiness checks
[OK] Creating probe VM                                                                                                                                                   
[OK] Waiting for probe VM RUNNING state                                                                                                                                  
[OK] Waiting for probe VM context                                                                                                                                        
[OK] Checking OneGate access                                                                                                                                             
[OK] Checking Internet connectivity                                                                                                                                      
[OK] Checking private network paths                                                                                                                                      
[OK] Cleanup probe VM                                                                                                                                                    
[OK] All OneKS readiness checks passed
```
    
# Congratulations, you've completed the assignment!
{: .no_toc}

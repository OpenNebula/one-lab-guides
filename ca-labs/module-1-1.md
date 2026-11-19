---
layout: default
title: Lab 1 - Frontend Node
parent: Module 1 - Introduction
---

# Module 1 - Lab 1 : Introduction
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

- Inspect the installed packages.
- Login to the Sunstone UI as oneadmin.

# Install the opennebula-form package and inspect the running systemd services.

## 1.1.1

Connect to Node 1's using your Frontend FQDN (lab-X.opennebula.academy) with a **ubuntu** user. 

Look at the OpenNebula services:

```console
systemctl | grep opennebula
    opennebula-fireedge.service            loaded    active running   OpenNebula FireEdge Server
    opennebula-flow.service                loaded    active running   OpenNebula Flow Service
    opennebula-form.service                loaded    active running   OpenNebula Form Service
    opennebula-gate.service                loaded    active running   OpenNebula Gate Service
    opennebula-guacd.service               loaded    active running   OpenNebula Guacamole Server
    opennebula-hem.service                 loaded    active running   OpenNebula Hook Execution Service
    opennebula-ssh-agent.service           loaded    active running   OpenNebula SSH agent
    opennebula.service                     loaded    active running   OpenNebula Cloud Controller Daemon
    opennebula-showback.timer              loaded    active waiting   OpenNebula's periodic showback calculation
    opennebula-ssh-socks-cleaner.timer     loaded    active waiting   OpenNebula SSH persistent connection cleaner
```

## 1.1.2

Open the <a href="https://lab-X.opennebula.academy/fireedge/sunstone/" target="_blank">Sunstone UI</a> and login using the credentials (substitute X with your Lab ID and hit enter).

<img src="./../assets/ca-images/module1_lab1/s2.png">

# Congratulations, you've completed the assignment!
{: .no_toc}
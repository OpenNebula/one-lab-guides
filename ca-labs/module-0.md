---
layout: default
title: Module 0 - Getting familiar with the Lab Environment 
parent: Certified Administrator
---
# Module 0 - Lab 0: Getting familiar with the Lab Environment
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

# FQDNs & Credentials

Your lab consists of 3 nodes:

| Node Name     | Username (SSH) |  Comment |
|----------------- | -------- | --------- |
| lab-**X**-node1     | ubuntu |  Frontend Node (Node 1), backup server, NFS server   | 
| lab-**X**-node2    | ubuntu 	|  Node 2 |
| lab-**X**-node3 | ubuntu |    Node 3 |

where **X** is your unique lab number issued by the instructor.


# Access the Web GUI

The 1st Node is hosting the Frontend services including the Web GUI (Sunstone).

You need to access Sunstone using the following URL:

https://lab-X.opennebula.academy/fireedge/sunstone/

where **X** is your unique lab number issued by the instructor.


# Access the Frontend node using SSH

Certain activities in this lab guide will require you to use CLI tools or access Node 2 & Node 3.

Use SSH from your personal device to the Frontend server. Don't forget to substitute X with your unique number assigned by the instructor.

```console
ssh ubuntu@lab-X.opennebula.academy

ubuntu@lab-X-node1:~
```

# oneadmin account

You are going to use **oneadmin** account to perform all OpenNebula-related activities.

```console
sudo -i -u oneadmin

oneadmin@lab-X-node1:~$
```
---
layout: default
title: Lab 2 - Backup Datastore
parent: Module 5 - Storage
---
# Module 5 - Lab 1 : Backup Datastore
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

- Create a Backup (Restic) datastore.


# Create a Backup (Restic) datastore.

{: .warning}
> Please note that in this lab environment the **Frontend** node is acting as the backup server. In a real-life scenario the backup server must be on a separate node! **Therefore you don't need to make sure that the backup server is reachable!**

## 5.2.1

Press the **Create Datastore** to start the process.

<img src="./../assets/ca-images/module5_lab2/s1.png">

## 5.2.2

Set the **Datastore type** to **BACKUP** and the **Storage backend** to **Backup-Restic**.

You can name the datastore the way you wish.

<img src="./../assets/ca-images/module5_lab2/s2.png">

## 5.2.3

Set the cluster to **default**. 

<img src="./../assets/ca-images/module5_lab2/s3.png">

## 5.2.4

There are three important fields to configure:

- Set the **Restic password** to any value. This value will be used to encrypt the data at rest. 
- Set the **Restic SFTP server** to **lab-X-node1** where X is your unique Lab ID.
- Set the **Restic SFTP user** to **oneadmin**.

<img src="./../assets/ca-images/module5_lab2/s4.png">

## 5.2.5

Leave **Custom Variables** as is and finish the process.

<img src="./../assets/ca-images/module5_lab2/s5.png">


## 5.2.6

You shold end up with another datastore added. Refresh the page and make sure it is monitored and the disk space metrics are gathered! 

<img src="./../assets/ca-images/module5_lab2/s6.png">

# Congratulations, you've completed the assignment!
{: .no_toc}
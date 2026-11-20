---
layout: default
title: Lab 1 - User Management
parent: Module 2 - Users, Groups and Permissions
---
# Module 2 - Lab 1 : User 
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
- Add a new User to the Group.
- Share the VM Template and an Image with the group.
- Enroll the **SSH Public Key**.

# Add a new User to the Group

## 1.1.1

Open the Browser and navigate to http://172.18.0.1

<img src="./../assets/cp-images/module2_lab1/s1.png">

## 1.1.2

Login using the **cloud-admin** user and the supplied credentials.

<img src="./../assets/cp-images/module2_lab1/s2.png">

## 1.1.3

Navigate to  **System - Users**.

<img src="./../assets/cp-images/module2_lab1/s3.png">

## 1.1.4

Press the **Create User** button.

<img src="./../assets/cp-images/module2_lab1/s4.png">

## 1.1.5

In the **Username** field set **cloud-user**.

Leave the ** Authentication Type** as is.

Set **Password** and **Confirm Password** field to your preferred password and press the **Next** button. 

<img src="./../assets/cp-images/module2_lab1/s5.png">

## 1.1.6

On the Primary Group configuration screen select the **cloud-users** group. 

<img src="./../assets/cp-images/module2_lab1/s6.png">

## 1.1.7

Leave the Secondary Group configuration screen as is and proceed to finish the wizard.

<img src="./../assets/cp-images/module2_lab1/s7.png">

## 1.1.8

You must end up with two users.

<img src="./../assets/cp-images/module2_lab1/s8.png">

# Share the VM Template and an Image with the group.

## 1.1.9

Navigate to **Templates -> VM Templates**. 

<img src="./../assets/cp-images/module2_lab1/s9.png">

## 1.1.10

Locate and select the **Alpine Linux 3.20** from the list.

<img src="./../assets/cp-images/module2_lab1/s10.png">

## 1.1.11

Update the permissions by checking both **USE** and **MANAGE** boxes. 

<img src="./../assets/cp-images/module2_lab1/s11.png">

## 1.1.12

Now members of the group can use and edit this resource. 

<img src="./../assets/cp-images/module2_lab1/s12.png">

## 1.1.13

Next navigate to **Storage -> Images**.

<img src="./../assets/cp-images/module2_lab1/s13.png">

## 1.1.14

Then locate and select the **Alpine Linux 3.20** image. 

<img src="./../assets/cp-images/module2_lab1/s14.png">

## 1.1.15

Perform the same update as you did with the VM Template by ticking the **USE** and **MANAGE** checkboxes.

<img src="./../assets/cp-images/module2_lab1/s15.png">

# Enroll the SSH Public Key

## 1.1.16

Sign out from the **cloud-admin** user.

<img src="./../assets/cp-images/module2_lab1/s16.png">

## 1.1.17

Sign in as the **cloud-user**. 

<img src="./../assets/cp-images/module2_lab1/s17.png">

## 1.1.18

Expand the user actions menu and Go to **Profile Settings**.

<img src="./../assets/cp-images/module2_lab1/s18.png">

## 1.1.19

Switch to **Security** tab. 

<img src="./../assets/cp-images/module2_lab1/s19.png">

## 1.1.20

From the **Applications** menu select the **Terminal Emulator**.

<img src="./../assets/cp-images/module2_lab1/s20.png">

## 1.1.21

Use the **cat** command to print the public key contents. 


```console
cat ~/.ssh/id_ed25519.pub
```
{: .warning }
> Note that your public key will be different than the one in the example

```console
ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIO5qvkt1J27fSE3++oCjX3Q0cP069oUOEiKwluzHky/Z root@ip-192-168-98-58
```

Copy the contents to the clipboard!

## 1.1.22

Now press the edit button near by the **SSH public key** field and paste the copied contents. 

<img src="./../assets/cp-images/module2_lab1/s22.png">


## 1.1.23

Then click anywhere outside of the textbox to save changes.

# Congratulations, you've completed the assignment!
{: .no_toc}
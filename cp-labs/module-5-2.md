---
layout: default
title: Lab 2 - Virtual Network Templates
parent: Module 5 - Network Reservations and Network Templates
---
# Module 5 - Lab 2 : Virtual Network Templates
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
- Instantiate the Virtual Network Template

# Create a Virtual Network Reservation

## 5.1.1

Navigate to **Networks -> Network Templates**.

<img src="./../assets/cp-images/module5_lab2/s1.png">

## 5.1.2

Locate and select the VN Template nmed **isolated**.

<img src="./../assets/cp-images/module5_lab2/s2.png">

## 5.1.3

Press the **Play** button.

<img src="./../assets/cp-images/module5_lab2/s3.png">

## 5.1.4

Name it **cloud-user-isolated** and proceed to the **Next** screen.

<img src="./../assets/cp-images/module5_lab2/s4.png">

## 5.1.5

Switch to the **Addresses** tab and press the **Add Address Range** button. 

<img src="./../assets/cp-images/module5_lab2/s5.png">

## 5.1.6

Set the **First IPv4 address** to **10.80.90.1**. 

Set the **Size** to **200**.

Press the **Accept** button.

<img src="./../assets/cp-images/module5_lab2/s6.png">

## 5.1.7

Keep all other settings as is and press the **Finish** button.

<img src="./../assets/cp-images/module5_lab2/s7.png">

## 5.1.8

Navigate to **Networks -> Virtual Networks**

<img src="./../assets/cp-images/module5_lab2/s8.png">

## 5.1.9

You should end up having three networks, two of them owned by **cloud-user**.

<img src="./../assets/cp-images/module5_lab2/s9.png">

# Congratulations, you've completed the assignment!
{: .no_toc}
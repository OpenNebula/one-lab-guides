---
layout: default
title: Lab 1 - Virtual Network Reservation
parent: Module 5 - Network Reservations and Network Templates
---
# Module 5 - Lab 1 : Virtual Network Reservation
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
- Create a Virtual Network Reservation
- Update the DNS attribute

# Create a Virtual Network Reservation

## 5.1.1

Navigate to **Networks -> Virtual Networks**.

<img src="./../assets/cp-images/module5_lab1/s1.png">

## 5.1.2

Locate and select the **vnet** Virtual Network.

<img src="./../assets/cp-images/module5_lab1/s2.png">

## 5.1.3

Press the **Reserve** button. 

<img src="./../assets/cp-images/module5_lab1/s3.png">

## 5.1.4

Set the **Number of addresses** to 10.

And the **Name** field to **cloud-user-public**.

Leave all other fields as is and press the **Accept** button.

<img src="./../assets/cp-images/module5_lab1/s4.png">

## 5.1.5

You might need to refresh the page for the new network to appear in the list.

The **vnet** now must have 10/100 addresses used.

<img src="./../assets/cp-images/module5_lab1/s5.png">

# Update the DNS attribute

## 5.1.6

Select the **cloud-user-public**. 

<img src="./../assets/cp-images/module5_lab1/s6.png">

## 5.1.7

Scroll down to the **Atributes** section and enter the **DNS** as the key and ***1.1.1.1** as the value.

Then press the **+** button to add/update the attribute.

<img src="./../assets/cp-images/module5_lab1/s7.png">

## 5.1.8

Once saved - the DNS key must now be equal to the new value. 

<img src="./../assets/cp-images/module5_lab1/s8.png">

# Congratulations, you've completed the assignment!
{: .no_toc}
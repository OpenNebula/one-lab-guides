---
layout: default
title: Lab 3 - Image Management
parent: Module 5 - Storage
---
## Module 5 - Lab 3 : Image Management
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
- Download an Image from the Marketplace.
- Import an Image from the URL.
- Change the Persitency of an Image.

# Download Images from the Marketplace.

## 5.3.1

Navigate to **Storage -> Apps** to access the list of available Images from all  Marketplaces. 

<img src="./../assets/ca-images/module5_lab3/s1.png">
    
## 5.3.2

In the search bar enter **Alpine Linux 3.21** and locate the **Alpine Linux 3.21** image. 

Please select the **correct architecture**!

<img src="./../assets/ca-images/module5_lab3/s2.png">
    
## 5.3.3

Press the Import button.

<img src="./../assets/ca-images/module5_lab3/s3.png">
    
## 5.3.4

Keep the names as is, then proceed to the next page of the wizard.

<img src="./../assets/ca-images/module5_lab3/s4.png">
    
## 5.3.5

From the datastores select the **shared image datastore** one and press **Finish**.

<img src="./../assets/ca-images/module5_lab3/s5.png">

# Import an Image from the URL.
    
## 5.3.6

Navigate to the **Storage -> Images**.

<img src="./../assets/ca-images/module5_lab3/s6.png">
    
## 5.3.7

Press **Create Image** to start the wizard.

<img src="./../assets/ca-images/module5_lab3/s7.png">
    
## 5.3.8

Name image as **Alpine Linux DB Server**.

Set the URL to the one provided by your instructor.

<img src="./../assets/ca-images/module5_lab3/s8.png">
    
## 5.3.9

Select the shared image datastore and proceed to the next screen.

<img src="./../assets/ca-images/module5_lab3/s9.png">

    
## 5.3.10

Set the **BUS** to **Virtio**.

<img src="./../assets/ca-images/module5_lab3/s10.png">

## 5.3.11

Keep the **Custom Atributes**  empty and press **Finish**

<img src="./../assets/ca-images/module5_lab3/s11.png">

# Share Images and Change the Persitency of an Image.
    
## 5.3.12

Select the Alpine Linux 3.21 image

<img src="./../assets/ca-images/module5_lab3/s12.png">

## 5.3.13

Then press the **Persistent** button.
    
<img src="./../assets/ca-images/module5_lab3/s13.png">

## 5.3.14

After that confirm the mode change.
    
<img src="./../assets/ca-images/module5_lab3/s14.png">

## 5.3.15

The image must become **Persistent**.

<img src="./../assets/ca-images/module5_lab3/s15.png">

## 5.3.16 

{: .note}
> Now perform the same action, but with the second Alpine Linux-based Image. 
> You should end up with two images in the **Persistent** mode. 
    
# Congratulations, you've completed the assignment!
{: .no_toc}
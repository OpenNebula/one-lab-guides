---
layout: default
title: Lab 3 - Deploy and Manage the VMs
parent: Module 8 - VM Templates & VMs
---
# Module 8 - Lab 3 : Deploy and Manage the VMs

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
- Deploy the Database VM.
- Deploy the Application VM.
- Verify the deployed Application.

# Deploy the Database VM.

## 8.3.1

Navigate to **Instances -> VMs**.

<img src="./../assets/ca-images/module8_lab3/s1.png">

## 8.3.2

Press the **Create VM** button.

<img src="./../assets/ca-images/module8_lab3/s2.png">

## 8.3.3

Select the **alpine-db-server** from the list.

<img src="./../assets/ca-images/module8_lab3/s3.png">

## 8.3.4

Keep the **Configuration** screen as is and proceed ot the next page.

<img src="./../assets/ca-images/module8_lab3/s4.png">

## 8.3.5

On the **User Inputs** page leave the input as is or enter the compatible timezone. For example - **Europe/Madrid**.

<img src="./../assets/ca-images/module8_lab3/s5.png">

## 8.3.6

On the **User Inputs** page leave the input as is or enter the compatible timezone. For example - **Europe/Madrid**.

<img src="./../assets/ca-images/module8_lab3/s6.png">

## 8.3.7

Wait until the VM is in the **Running** state and an IP address has been assigned. 

Copy the IP address - you will need it in the further steps. 

<img src="./../assets/ca-images/module8_lab3/s7.png">

# Deploy the Application VM.

## 8.3.8

Back on the VMs page - press the **Create VM** button.

<img src="./../assets/ca-images/module8_lab3/s8.png">

## 8.3.9

From the VM Template list select the **alpine-app-server** VM Template.

<img src="./../assets/ca-images/module8_lab3/s9.png">
    
## 8.3.10

Keep the Configuration as is and proceed to **User inputs**.

<img src="./../assets/ca-images/module8_lab3/s10.png">
    
## 8.3.11

Set the **DB_HOST** to the IP Address of the **alpine-db-server** VM you have extracted before.

Set the **DB_PASSWORD** to **appassword** and leave rest as is.

<img src="./../assets/ca-images/module8_lab3/s11.png">

## 8.3.12

Go to the **Placement** tab and make sure to select the **app-cluster** cluster.

<img src="./../assets/ca-images/module8_lab3/s12.png">

{: .note}
> It may take some time to start the VM + there's an internal sleep time to 60 seconds in the Start script. Return back in 3 to 5 minutes to proceed with the lab.
    
## 8.3.13

In the **Attributes** locate the **CFD_URL** attribute and copy the value.

<img src="./../assets/ca-images/module8_lab3/s13.png">

# Verify the deployed Application.
  
## 8.3.14

Open the URL in the new tab.

<img src="./../assets/ca-images/module8_lab3/s14.png">
    
## 8.3.15

Press the **Create the Travel Log** button.

<img src="./../assets/ca-images/module8_lab3/s15.png">
   
## 8.3.16

{: .note}
> You **must get the success message, otherwise stop and debug the connectivity between your VMs**.

Press **Return to Helm**.

<img src="./../assets/ca-images/module8_lab3/s16.png">
    
## 8.3.17

Press the middle button to create a record in the Log.

<img src="./../assets/ca-images/module8_lab3/s17.png">

## 8.3.18

You must get the success message. 

Press the **Log Another Travel** button a few times to create more records.

Once ready - press the **Return to Helm** button. 

<img src="./../assets/ca-images/module8_lab3/s18.png">
   
## 8.3.19

Lastly we must request the data!

Press **Read the Travel Log**.

<img src="./../assets/ca-images/module8_lab3/s19.png">					

## 8.3.20

Your data must be printed.

<img src="./../assets/ca-images/module8_lab3/s20.png">	
  
# Congratulations, you've completed the assignment!
{: .no_toc}
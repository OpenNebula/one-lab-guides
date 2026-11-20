---
layout: default
title: Lab 1 - Virtual Machine Templates
parent: Module 6 - VM Templates & VMs
---
# Module 6 - Lab 1 : Virtual Machine Templates
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
- Clone the Alpine Linux VM Template
- Rename the Ubuntu 24.04 VM Template
- Update the alpine-app VM Template
- Update the ubuntu-cloudflared VM Template

# Clone the Alpine Linux VM Template

## 6.1.1

Navigate to **Templates -> VM Templates**.

<img src="./../assets/cp-images/module6_lab1/s1.png">

## 6.1.2

Locate and select the **Alpine Linux 3.20**.

<img src="./../assets/cp-images/module6_lab1/s2.png">

## 6.1.3

Press the **Clone** button.

<img src="./../assets/cp-images/module6_lab1/s3.png">

## 6.1.4

Mane it **alpine-app** and make sure that the **Clone with images** checkbox is not selected. 

Press the **Clone** button to confirm the intent.

<img src="./../assets/cp-images/module6_lab1/s4.png">

## 6.1.5

You must end up with three templates where two of them are owned by **cloud-user**.

<img src="./../assets/cp-images/module6_lab1/s5.png">

# Rename the Ubuntu 24.04 VM Template

## 6.1.6

Locate and select the **Ubuntu 24.04** VM Template.

<img src="./../assets/cp-images/module6_lab1/s6.png">

## 6.1.7

Press the **Rename** button.

<img src="./../assets/cp-images/module6_lab1/s7.png">

## 6.1.8

Set the name to **ubuntu-cloudflared** and press anywhere outside of the field to save changes.

<img src="./../assets/cp-images/module6_lab1/s8.png">

## 6.1.9

You should end up with two custom named VM Templates.

<img src="./../assets/cp-images/module6_lab1/s9.png">

# Update the alpine-app VM Template

## 6.1.10

Locate and select the **alpine-app** VM Template.

<img src="./../assets/cp-images/module6_lab1/s10.png">

## 6.1.11

Press the **Update** button.

<img src="./../assets/cp-images/module6_lab1/s11.png">

## 6.1.12

Set the **Memory** value to **1GB** and proceed to the next page.

<img src="./../assets/cp-images/module6_lab1/s12.png">

## 6.1.13

Go to **Context** section.

<img src="./../assets/cp-images/module6_lab1/s13.png">

## 6.1.14

Scroll down to **Start script** and paste the following code.

```console
rc-service apache2 start
```

<img src="./../assets/cp-images/module6_lab1/s14.png">

## 6.1.15

Scroll further down and locate the **User inputs** section.

Set **Name** to **TIMEZONE**.

Keep **Type** as **Text**.

Optionally set the **Description**

Set **Default value** to **UTC**.

And press the **Add** button.

<img src="./../assets/cp-images/module6_lab1/s15.png">

## 6.1.16

You must end up with the User input prompt added.

<img src="./../assets/cp-images/module6_lab1/s16.png">

## 6.1.17

Scroll further down and locate the **Context Custom Variables**.

Set the key to **SET_HOSTNAME** and the value to **$NAME**. 

Click the **+** button to add the variable.

<img src="./../assets/cp-images/module6_lab1/s17.png">

## 6.1.18

Make sure that the variable has been added and click the **Save** button.

<img src="./../assets/cp-images/module6_lab1/s18.png">

# Update the ubuntu-cloudflared VM Template

## 6.1.19 

Locate and select the **ubuntu-cloudflared** VM Template.

<img src="./../assets/cp-images/module6_lab1/s19.png">

## 6.1.20

Press the **Update** button.

<img src="./../assets/cp-images/module6_lab1/s20.png">

## 6.1.21

Keep the **General** settings as is and click the **Next** button.

<img src="./../assets/cp-images/module6_lab1/s21.png">

## 6.1.22

Switch to the **Context** tab and make sure that the **Add OneGate token** is toggled.

<img src="./../assets/cp-images/module6_lab1/s22.png">

## 6.1.23

Scroll further down and paste the following code into the **Start script** field.

```console
cloudflared tunnel --url http://$APP_IP > /var/log/cfd.log 2>&1 &
sleep 60
export CFD=$(grep -o -e 'https.*trycloudflare.com' /var/log/cfd.log)
onegate vm update $VMID --data CFD_URL=$CFD
```
<img src="./../assets/cp-images/module6_lab1/s23.png">

## 6.1.24

Scroll further down and locate the **User inputs** section.

Set the **Name** to **APP_IP**.

Keep the **Type** as Text.

Optionally add the **Description**.

Set the **Default value** to **127.0.0.1**.

Make sure the **Mandatory** is toggled.

And click the **+** button.

<img src="./../assets/cp-images/module6_lab1/s24.png">

## 6.1.25

Make sure that the input has been added.

<img src="./../assets/cp-images/module6_lab1/s25.png">

## 6.1.26

Scroll further down to the **Context Custom Variables** section and add a new variable with the key **SET_HOSTNAME** and the value to **$NAME**.

<img src="./../assets/cp-images/module6_lab1/s26.png">

## 6.1.27

Make sure tha the variable has been added and click the **Save** button.

# Congratulations, you've completed the assignment!
{: .no_toc}
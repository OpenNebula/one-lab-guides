---
layout: default
title: Lab 2 - Custom VMs
parent: Module 6 - VM Templates & VMs
---
# Module 6 - Lab 2 : Custom VMs
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
- Instantiate VM Templates
- Execute customization scripts
- Verify that images are working as expected

# Instantiate VM Templates

## 6.2.1

Navigate to **Instances -> VMs**.

<img src="./../assets/cp-images/module6_lab2/s1.png">

## 6.2.2

Click the **Create VM** button.

<img src="./../assets/cp-images/module6_lab2/s2.png">

## 6.2.3

Select the **alpine-app** from the VM Template list.

<img src="./../assets/cp-images/module6_lab2/s3.png">

## 6.2.4

Keep the **Configuration** as is and click **Next**.

<img src="./../assets/cp-images/module6_lab2/s4.png">

## 6.2.5

Optionally set the timezone and proceed to the **Next** screen.

<img src="./../assets/cp-images/module6_lab2/s5.png">

## 6.2.6

Keep all **Advanced parameters** as is and click **Finish**.

<img src="./../assets/cp-images/module6_lab2/s6.png">

## 6.2.7

A VM will be in the **Running** state shortly.

<img src="./../assets/cp-images/module6_lab2/s7.png">

## 6.2.8

Press the **Create VM**.

<img src="./../assets/cp-images/module6_lab2/s8.png">

## 6.2.9

Select the **ubuntu-cloudflared** VM Template from the list. 

<img src="./../assets/cp-images/module6_lab2/s9.png">

## 6.2.10

Keep the **Configuration** as is and click **Next**.

<img src="./../assets/cp-images/module6_lab2/s10.png">

## 6.2.11

Keep the **User inputs** as is and proceed to the **Advanced options**. 

<img src="./../assets/cp-images/module6_lab2/s11.png">

## 6.2.12

Switch to **Network** tab and press the **Attach NIC** button.

<img src="./../assets/cp-images/module6_lab2/s12.png">

## 6.2.13

Keep the **Advanced options** as is.

<img src="./../assets/cp-images/module6_lab2/s13.png">

## 6.2.14

Select the **cloud-user-public** Virtual Network and proceed to the **Next** screen.

<img src="./../assets/cp-images/module6_lab2/s14.png">

## 6.2.15

Keep the **Network values** as is.

<img src="./../assets/cp-images/module6_lab2/s15.png">

## 6.2.16

Keep the **QoS** as is and click the **Finish** button.

<img src="./../assets/cp-images/module6_lab2/s16.png">

## 6.2.17

Now attach another NIC, but this time place it into the **cloud-user-isolated** network.

<img src="./../assets/cp-images/module6_lab2/s17.png">

## 6.2.18

Press the **Finish** button. 

<img src="./../assets/cp-images/module6_lab2/s18.png">

## 6.2.19

Write down the IP Addresse of the VMs.

<img src="./../assets/cp-images/module6_lab2/s19.png">

{: .note }
> Note that your IPs might differ.

# Execute customization scripts

## 6.2.20

Open the **Terminal** window and connect to the **alpine-app** first.

```console
ssh root@172.17.100.3
```

Once connected install apache2

```console
apk add apache2
```

Once installed - exit the VM.

```console
exit
```

## 6.2.21

Now connect to the **ubuntu-cloudflared** VM using the SSH.

```console
ssh root@172.16.100.2
```

Once connected - execute the following set of commands

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set VMs
git checkout
cd VMs
chmod +x prep_clfd.sh
./prep_clfd.sh
cloudflared --help
```

The output should show the cloudflared help.

```console
...
COPYRIGHT:
   (c) 2026 Cloudflare Inc.
   Your installation of cloudflared software constitutes a symbol of your signature indicating that you accept
   the terms of the Apache License Version 2.0 (https://developers.cloudflare.com/cloudflare-one/connections/connect-apps/license),
   Terms (https://www.cloudflare.com/terms/) and Privacy Policy (https://www.cloudflare.com/privacypolicy/).
```

Exit the VM.

```console
exit
```

# Verify that images are working as expected

## 6.2.22

Select the **ubuntu-cloudflared** VM and switch to the **Configuration** tab

<img src="./../assets/cp-images/module6_lab2/s22.png">

## 6.2.23

Press the **Update configuration** button.

<img src="./../assets/cp-images/module6_lab2/s23.png">

## 6.2.24

Go to the **Context**.

<img src="./../assets/cp-images/module6_lab2/s24.png">

## 6.2.25

Scroll down to the **Context Custom Variables** section and update the **APP_IP** key with the **alpine-app** IP as the value.

Press **+** to update the variable.

<img src="./../assets/cp-images/module6_lab2/s25.png">

## 6.2.26

Make sure that the value has been saved and click **Continue**.

<img src="./../assets/cp-images/module6_lab2/s26.png">

## 6.2.27

Then open the **VM state** drop-down menu and **Reboot** the VM.

<img src="./../assets/cp-images/module6_lab2/s27.png">

## 6.2.28

Confirm the intention to reboot and wait approximately 5 minutes. 

<img src="./../assets/cp-images/module6_lab2/s28.png">

## 6.2.29

Switch to the **Info** tab and scroll down until you will locate the **CFD_URL** attribute. 

Copy the address!

<img src="./../assets/cp-images/module6_lab2/s29.png">

## 6.2.30

Open the new tab and navigate to the copied URL.

You supposed to see the Apache2 httpd's dummy page.

<img src="./../assets/cp-images/module6_lab2/s30.png">

# Terminate VMs and change the Persistency

## 6.2.31

Return back to Sunstone and select both VMs.

<img src="./../assets/cp-images/module6_lab2/s31.png">

## 6.2.32

Click the **trash bin** icon and select **Terminate**.

<img src="./../assets/cp-images/module6_lab2/s32.png">

## 6.2.33

Confirm the intention to terminate both VMs.

<img src="./../assets/cp-images/module6_lab2/s33.png">

## 6.2.34

Wait until VMs are in **Done** state.

<img src="./../assets/cp-images/module6_lab2/s34.png">

## 6.2.35

Navigate to **Storage - Images**.

<img src="./../assets/cp-images/module6_lab2/s35.png">

## 6.2.36

Select both images.

<img src="./../assets/cp-images/module6_lab2/s36.png">

## 6.2.37

And make them **Non Persistent**!

<img src="./../assets/cp-images/module6_lab2/s37.png">

## 6.2.38

Make sure to confirm the action.

<img src="./../assets/cp-images/module6_lab2/s38.png">

## 6.2.39

The persistency label should disappear and your images are now ready to be deployed at scale!

<img src="./../assets/cp-images/module6_lab2/s39.png">

# Congratulations, you've completed the assignment!
{: .no_toc}
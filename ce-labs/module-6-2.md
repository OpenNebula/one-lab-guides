---
layout: default
title: Lab 2 - Provision the Kubernetes Cluster
parent: Module 6 - OneKS
---
# Module 6 - Lab 2 : Provision the Kubernetes Cluster
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
- Provision the Control Plane
- Provision a Node Group
- Extract the kubeconfig
- Install the CSI and create the Storage Class
- Deploy the Test App
- Remove the deployment and cleanup the cluster.


# Provision the Control Plane.
     
## 6.2.1

In Sunstone, navigate to **Kubernetes -> K8S Cluster**.

<img src="./../assets/ce-images/module6_lab2/s1.png">

## 6.2.2

Press **Create Kubernetes Cluster**.

<img src="./../assets/ce-images/module6_lab2/s2.png">

## 6.2.3

Name it the way you wish and proceed to the next page. 

<img src="./../assets/ce-images/module6_lab2/s3.png">

## 6.2.4

Select the **default** cluster from the list.

<img src="./../assets/ce-images/module6_lab2/s4.png">

## 6.2.5

Map the **Public network** to the **routable** network.

<img src="./../assets/ce-images/module6_lab2/s5.png">

## 6.2.6

Map the **Private network** to the **public** network.

<img src="./../assets/ce-images/module6_lab2/s6.png">

## 6.2.7

Select the Kubernetes version.

<img src="./../assets/ce-images/module6_lab2/s7.png">

## 6.2.8

Select the **Single-Node** cluster type.

<img src="./../assets/ce-images/module6_lab2/s8.png">

## 6.2.9

Because default state of User inputs forbidds users to alter these settings - simply press the **Finish** button.

<img src="./../assets/ce-images/module6_lab2/s9.png">

## 6.2.10

Wait until the the control plane is in the **Running** state. 

<img src="./../assets/ce-images/module6_lab2/s10.png">

# Provision a Node Group

## 6.2.11

Select the lab-cluster and switch to the **Node Group**.

<img src="./../assets/ce-images/module6_lab2/s11.png">

## 6.2.12

Press the **Create Node Group** button.

<img src="./../assets/ce-images/module6_lab2/s12.png">

## 6.2.13

Name it the way you wish and proceed to the next page.

<img src="./../assets/ce-images/module6_lab2/s13.png">

## 6.2.14

Select the **Small Worker Nodes**.

<img src="./../assets/ce-images/module6_lab2/s14.png">

## 6.2.15

Set the **Count** value to 2 and press the **Finish** button.
    
<img src="./../assets/ce-images/module6_lab2/s15.png">

## 6.2.16

Wait until the state will be changed from **scaling** to **running**.

<img src="./../assets/ce-images/module6_lab2/s16.png">

# Extract the kubeconfig

## 6.2.17

Open the k8s cluster and switch to the **Kubeconfig** tab, then press the **copy** button.

<img src="./../assets/ce-images/module6_lab2/s17.png">

## 6.2.18 

{: .note }
> Further steps must be performed on the VDI, therfore make sure you are NOT CONNECTED to the Frontend node. For assurance you may close the terminal windows and open it again!

Execute the whoami command.
```console
whoami
```

Make sure you are the **abc user**.

```console
abc
```

## 6.2.19

Create the .kube directory.

```console
mkdir ~/.kube
```

Open the config file in your prefereed editor. You may leverage VSCodium for should you need to. 

```console
vi ~/.kube/config
```

Paste the kubeconfig into the file and save the changes.

## 6.2.20

Run the kubectl to verify that the kubeconfig is correct.

```console
kubectl get nodes
```

Make sure your output displays one control plane and two nodes.

```console
NAME                                                 STATUS   ROLES                AGE   VERSION
controlplane-general-standalone-3123c60e2a36-5sjsr   Ready    control-plane,etcd   10h   v1.34.2+rke2r1
nodegroup-general-small-e447be1484f2-sxkvs-nxb6b     Ready    <none>               15m   v1.34.2+rke2r1
nodegroup-general-small-e447be1484f2-sxkvs-qjxz7     Ready    <none>               15m   v1.34.2+rke2r1
```

# Install the CSI and create the Storage Class

## 6.2.21

Firstly create the secrets store that will be used for authentication. **Make sure to set the correct password!**

```console
kubectl -n kube-system create secret generic opennebula-csi-auth --from-literal=credentials='oneadmin:<PASSWORD>'
```

You should get the confirmation message.

```console
secret/opennebula-csi-auth created
```

## 6.2.22

Add the repository that contains the Helm Chart.

```console
helm repo add opennebula https://opennebula.github.io/storage-provider-opennebula/charts/
helm repo update
```

Make sure that the output looks like the one below

```console
"opennebula" has been added to your repositories
Hang tight while we grab the latest from your chart repositories...
...Successfully got an update from the "opennebula" chart repository
Update Complete. ⎈Happy Helming!⎈
```

## 6.2.23

Install the CSI using Helm Charts.

```console
helm upgrade --install opennebula-csi opennebula/opennebula-csi \
  --namespace kube-system \
  --create-namespace \
  --set credentials.existingSecret.name=opennebula-csi-auth \
  --set oneApiEndpoint=http://169.254.16.9:2633/RPC2
```

You should have the confirmation that the chart has been installed.

```console
Release "opennebula-csi" does not exist. Installing it now.
NAME: opennebula-csi
LAST DEPLOYED: Mon Sep 14 21:43:59 2026
NAMESPACE: kube-system
STATUS: deployed
REVISION: 1
DESCRIPTION: Install complete
TEST SUITE: None
```

## 6.2.24

Create a file one-sc.yaml.

```console
vi one-sc.yaml
```

And paste the following content.

```console
driver:
  defaultDatastores:
    - "1"

storageClasses:
  - name: opennebula-csi
    reclaimPolicy: Delete
    allowVolumeExpansion: true
    volumeBindingMode: WaitForFirstConsumer
    parameters:
      datastoreIDs: "1"
      fsType: "ext4"
      driver: "qcow2"
```

And then apply the Storage Class.

```console
helm upgrade opennebula-csi opennebula/opennebula-csi \
  --namespace kube-system \
  -f one-sc.yaml \
  --reuse-values
```

Make sure there are no errors in the output:

```console
Release "opennebula-csi" has been upgraded. Happy Helming!
NAME: opennebula-csi
LAST DEPLOYED: Mon Sep 14 21:50:33 2026
NAMESPACE: kube-system
STATUS: deployed
REVISION: 2
DESCRIPTION: Upgrade complete
TEST SUITE: None
```

## 6.2.25

Clone the repository with files.

```console
export REPO='https://github.com/OpenNebula/one-training-files.git'
rm -rf ~/Files
git clone --no-checkout $REPO  ~/Files
cd ~/Files
git sparse-checkout init --cone
git sparse-checkout set OneKE
git checkout
cd OneKE
```

Wait until the clone is complete.

```console
Cloning into '/config/Files'...
remote: Enumerating objects: 197, done.
remote: Counting objects: 100% (27/27), done.
remote: Compressing objects: 100% (26/26), done.
remote: Total 197 (delta 1), reused 1 (delta 1), pack-reused 170 (from 1)
Receiving objects: 100% (197/197), 276.70 KiB | 7.48 MiB/s, done.
Resolving deltas: 100% (81/81), done.
Your branch is up to date with 'origin/master'.
```

Make sure you have the correct set of files.

```console
ls -lh

total 28K
drwxr-xr-x 2 abc users 4.0K Sep 14 21:52 test-app
drwxr-xr-x 2 abc users 4.0K Sep 14 21:52 test-app-v2-cloudflared
-rw-r--r-- 1 abc users 7.0K Sep 14 21:52 test-app-v2-cloudflared.tar
drwxr-xr-x 2 abc users 4.0K Sep 14 21:52 test-app-v2-lb
-rw-r--r-- 1 abc users  640 Sep 14 21:52 test-app-v2-lb.tar
-rw-r--r-- 1 abc users  943 Sep 14 21:52 test-app.tar
```

## 2.6.26

Create the PersistentVolumeClaim file.

```console
cd test-app-v2-lb
vi mariadb-pvc.yaml
```

Paste the following contents into the file.

```console
apiVersion: v1
kind: PersistentVolumeClaim
metadata:
  name: mariadb-data
spec:
  accessModes:
    - ReadWriteOnce
  storageClassName: opennebula-csi
  resources:
    requests:
      storage: 2Gi
```

Save the file.

## 2.6.27

Open the **mariadb-deployment.yaml** file in the preferred editor and append the following to the end of the file.

```console
          volumeMounts:
            - name: mariadb-data
              mountPath: /var/lib/mysql
      volumes:
        - name: mariadb-data
          persistentVolumeClaim:
            claimName: mariadb-data
```
Save the file.

# Deploy the Test App 

## 2.6.28

Execute the **kubectl** command.

```console
kubectl apply -f .
```

And make sure your ouput looks like the one below.

```console
deployment.apps/mariadb created
persistentvolumeclaim/mariadb-data created
service/mariadb created
deployment.apps/test-app created
service/test-app-exposed created
```

## 2.6.29

Check if pods were created without issues.

```console
kubectl get pods
```

All pods should be running.

```console
NAME                        READY   STATUS    RESTARTS   AGE
mariadb-5c58998f57-6r6ms    1/1     Running   0          65s
test-app-6fc848875c-66dw8   1/1     Running   0          65s
test-app-6fc848875c-jct7w   1/1     Running   0          65s
```

Check if pvc has been added.

```console
NAME           STATUS   VOLUME                                     CAPACITY   ACCESS MODES   STORAGECLASS     VOLUMEATTRIBUTESCLASS   AGE
mariadb-data   Bound    pvc-bea656ed-f1d8-43b8-82bd-2f28bf11141a   2Gi        RWO            opennebula-csi   <unset>                 2m28s
```

Check if the service has been exposed.

```console
kubectl get svc
```

Make sure that the IP **test-app-exposed** LoadBalancer service has the IP address from the public subnet!

```console
NAME               TYPE           CLUSTER-IP     EXTERNAL-IP    PORT(S)        AGE
kubernetes         ClusterIP      10.43.0.1      <none>         443/TCP        10h
mariadb            ClusterIP      10.43.41.227   <none>         3306/TCP       4m32s
test-app-exposed   LoadBalancer   10.43.177.36   172.17.2.213   80:31218/TCP   4m32s
```

## 2.6.30

Copy the IP address and open it in the browser.

Press the **Create the Travel Log** button.

<img src="./../assets/ce-images/module6_lab2/s30.png">

## 2.6.31

Now press **Return to Helm** button.

<img src="./../assets/ce-images/module6_lab2/s31.png">

## 2.6.32

Press the **Log the Travel** button.

<img src="./../assets/ce-images/module6_lab2/s32.png">

## 2.6.33

Press the **Log Another Travel** a few times to generate the data.

<img src="./../assets/ce-images/module6_lab2/s33.png">

## 2.6.34

Now press **Return to Helm** button.

<img src="./../assets/ce-images/module6_lab2/s34.png">

## 2.6.35

Now press **Read the Travel Log** to open the data.

<img src="./../assets/ce-images/module6_lab2/s35.png">

## 2.6.36

The data supposed to be there.

<img src="./../assets/ce-images/module6_lab2/s36.png">

# Verify the PersistentVolume

## 2.6.38 

Return back to CLI and execute the kubectl to extract the mariadb pod name.

```console
kubectl get pods
```

Copy the pod name

```console
NAME                        READY   STATUS    RESTARTS   AGE
mariadb-5c58998f57-6r6ms    1/1     Running   0          15m
...
```

Execute the kubectl command to delete the pod.

```console
kubectl delete pod <POD NAME>
```

Your pod must be deleted

```console
pod "mariadb-5c58998f57-6r6ms" deleted from default namespace
```

## 2.6.39

Request the pods once again.

```console
kubectl get pods
```

The mariadb pod must be recreated!

```console
NAME                        READY   STATUS    RESTARTS   AGE
mariadb-5c58998f57-qwrqk    1/1     Running   0          40s
test-app-6fc848875c-66dw8   1/1     Running   0          17m
test-app-6fc848875c-jct7w   1/1     Running   0          17m
```

## 3.6.40

Return back to the test app in browser and refresh the page or press the **Read the Travel Log** button.

The data must be there despited the pod removal. This proves that the volume is persistent.

<img src="./../assets/ce-images/module6_lab2/s40.png">

## 2.6.41

Lastly, connect to the OpenNebula's Frontend Node and execute the oneimage list command.

```console
oneimage list
```

You should find the **pvc** image that is **persistent** and also resembles that name that you saw in the kubectl output.

```console
  ID USER     GROUP    NAME                                                   DATASTORE     SIZE TYPE PER STAT RVMS
   8 oneadmin oneadmin pvc-bea656ed-f1d8-43b8-82bd-2f28bf11141a               default         2G DB   Yes used    1
   ...
```

# Remove the deployment and cleanup the cluster.

## 2.6.42

Back to the kubectl - execute the delete command.

```console
kubectl delete -f .
```

Wait untill all objects are removed.

```console
deployment.apps "mariadb" deleted from default namespace
persistentvolumeclaim "mariadb-data" deleted from default namespace
service "mariadb" deleted from default namespace
deployment.apps "test-app" deleted from default namespace
service "test-app-exposed" deleted from default namespace
```

## 2.6.43

From the OpenNebula Frontend Node execute the **oneks** command.

```console
oneks list clusters
```

Note the id of a cluster.

```console
  ID USER     GROUP    NAME                                                    STATE                        REGTIME
   6 oneadmin oneadmin lab-cluster                                             RUNNING               09/14 11:12:14
```

## 2.6.44

Remove the cluster.

```console
oneks delete cluster <Cluster ID>
```

As a result all VMs must be removed from OpenNebula.

<img src="./../assets/ce-images/module6_lab2/s44.png">


# Congratulations, you've completed the assignment!
{: .no_toc}

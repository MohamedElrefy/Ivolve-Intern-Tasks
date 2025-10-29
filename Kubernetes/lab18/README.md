# Lab 18: Persistent Storage Setup for Application Logging

## Objective
Configure a Persistent Volume (PV) and Persistent Volume Claim (PVC) to store application logs persistently across Pods using Kubernetes **hostPath** storage.

---

##  Step 1 — Prepare Node Directory

Since we are using a `hostPath` volume, the storage directory must exist **on the worker node(s)** where the application Pod will run.

Run the following commands on each **worker node** or using Ansible:

```bash
sudo mkdir -p /mnt/app-logs
sudo chmod 777 /mnt/app-logs
```
This ensures that the path /mnt/app-logs exists and is accessible by all Pods.

## Step 2 — Create Persistent Volume (PV)
```bash
kubectl apply -f pv.yml
```
## Step 3 — Create Persistent Volume Claim (PVC)
```bash
kubectl apply -f pvc.yml
```
## Step 4 — Verify PV and PVC Status
```bash
kubectl get pv
kubectl get pvc
```
![alt text](<Screenshot from 2025-10-28 12-16-19.png>)



NOTE!!

When you don’t specify a storageClassName in the PVC, Kubernetes automatically assigns the default StorageClass,
 If your PV doesn’t have a storageClassName — it’s <unset>
 Therefore, they don’t match, and binding fails

 So you have two options :
 1 - Add storageClassName to the PV same as one assigned to the PVC

 2 - Explicitly in the PVC yaml file set:
   storageClassName: "" 
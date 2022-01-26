### Prisma Cloud: Securing GKE Run Time


```
&cloudshell=true
```


```

gcloud container clusters get-credentials k8-cluster --zone us-central1-a --project $DEVSHELL_PROJECT_ID
curl https://storage.googleapis.com/qwiklabs-code/prisma_cloud_compute_edition_21_04_421.tar.gz -o prisma_cloud_compute_edition_21_04_421.tar.gz
mkdir prisma_cloud_compute_edition
tar xvzf prisma_cloud_compute_edition_21_04_421.tar.gz -C prisma_cloud_compute_edition/
cd prisma_cloud_compute_edition
./linux/twistcli console export kubernetes --service-type LoadBalancer

```

After Giving Token 

```
kubectl create -f twistlock_console.yaml
kubectl get service -w -n twistlock

```
---
https://<YOUR-EXTERNAL-IP>:8083


```
admin
```

```
Pal0Alt0@123
```

---


1. Manage > Defenders
2. Deploy > Defender >> Orchestrator
```
twistlock-console
```
3. Nodes use Container Runtime Interface (CRI), not Docker.
4. Select target machine OS section----> Linux.

---
---
---


```
git clone https://github.com/PaloAltoNetworks/prisma_cloud; cd prisma_cloud
kubectl create namespace sock-shop
kubectl apply -f sock-shop.yaml
kubectl get service -n sock-shop -w

```
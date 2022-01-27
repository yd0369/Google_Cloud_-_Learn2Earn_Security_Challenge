### Prisma Cloud: Securing GKE Run Time


```
https://console.cloud.google.com/compute/instances?cloudshell=true
```


```

gcloud container clusters get-credentials k8-cluster --zone us-central1-a --project $DEVSHELL_PROJECT_ID
curl -O https://cdn.twistlock.com/releases/f7371a8b/prisma_cloud_compute_edition_20_09_345.tar.gz
mkdir prisma_cloud_compute_edition
tar xvzf prisma_cloud_compute_edition_20_09_345.tar.gz -C prisma_cloud_compute_edition/
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
3. Subject Alternative Names (SAN) click to add
4. Go to Manage > Defenders > Names.
5. Click Add SAN.
6. External IP address.
7. Click Add.

8. Manage > Defenders > Deploy > Single Defender
9. Access the console >>>>>> External IP
10. choose >>>>> Host Defender - Linux. 

---
---
---

```
gcloud beta compute ssh --zone "us-central1-b" "kali" --project $DEVSHELL_PROJECT_ID

```
```
gcloud beta compute ssh --zone "us-central1-b" "juice-shop" --project $DEVSHELL_PROJECT_ID

```
```
gcloud beta compute ssh --zone "us-central1-b" "jenkins-vm" --project $DEVSHELL_PROJECT_ID

```

---
---


1. Defend > Runtime > Host Policy
2. Rule name
```
prevent ls
```
3. Select all hosts
---
4. On the Processes tab, switch Effect from Alert to Prevent
5. prevented processess
```
ls
```
---
##### On the Networking tab:
1. Enable DNS
2. Turn Effect to Prevent
3. Add *.google.com to the Prevented domains list
```
*.google.com
```
4. save
---
---
---
only For Kali 

```
ls
nslookup www.google.com
nslookup www.paloaltonetworks.com

```

---

1. Defend > Runtime > Host Policy
2. Add Rule
```
ql-nov-10
```
3. Log Inspections
4. Add log path:
```
/var/log/nginx/access.log
```
5. Add inspection expression:
```
Mozilla
```



---
---
---


1. Defend > Runtime > Host Policy
2. Add Rule 
```
docker
```
3. Activities Tab
4. Docker Commands >>>>> ON

Add a new file integrity rule with the followings:

Path: 
```
/etc
```
- Write: checked
- Read: checked
- Metadata: checked
- scroll down and click Add File Integrity Rule

---


Only for Jenkins

```
sudo systemctl start docker
docker container create 3ac75179d901
sudo nano /etc/resolv.conf

```
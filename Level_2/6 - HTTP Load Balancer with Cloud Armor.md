https://www.cloudskillsboost.google/games/2289/labs/13146



https://www.cloudskillsboost.google/focuses/22771?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243365


```
https://console.cloud.google.com/net-services/loadbalancing/list/loadBalancers&cloudshell=true
```


```
gcloud compute firewall-rules create default-allow-http --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp:80 --source-ranges=0.0.0.0/0 --target-tags=http-server

gcloud compute firewall-rules create 	default-allow-health-check --direction=INGRESS --priority=1000 --network=default --action=ALLOW --rules=tcp --source-ranges=130.211.0.0/22,35.191.0.0/16 --target-tags=http-server

gcloud compute instance-templates create us-east1-template --project=qwiklabs-gcp-04-e1b626a44e68 --machine-type=n1-standard-1 --network-interface=network-tier=PREMIUM,subnet=default --metadata=startup-script-url=gs://cloud-training/gcpnet/httplb/startup.sh,enable-oslogin=true --maintenance-policy=MIGRATE --service-account=811692711742-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --region=us-east1 --tags=http-server --create-disk=auto-delete=yes,boot=yes,device-name=us-east1-template,image=projects/debian-cloud/global/images/debian-10-buster-v20220118,mode=rw,size=10,type=pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

gcloud compute instance-templates create europe-west1-template --project=qwiklabs-gcp-04-e1b626a44e68 --machine-type=n1-standard-1 --network-interface=network-tier=PREMIUM,subnet=default --metadata=startup-script-url=gs://cloud-training/gcpnet/httplb/startup.sh,enable-oslogin=true --maintenance-policy=MIGRATE --service-account=811692711742-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --region=europe-west1 --tags=http-server --create-disk=auto-delete=yes,boot=yes,device-name=europe-west1-template,image=projects/debian-cloud/global/images/debian-10-buster-v20220118,mode=rw,size=10,type=pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

gcloud beta compute instance-groups managed create us-east1-mig --project=qwiklabs-gcp-04-e1b626a44e68 --base-instance-name=us-east1-mig --size=1 --template=us-east1-template --zones=us-east1-b,us-east1-c,us-east1-d --target-distribution-shape=EVEN && gcloud beta compute instance-groups managed set-autoscaling us-east1-mig --project=qwiklabs-gcp-04-e1b626a44e68 --region=us-east1 --cool-down-period=45 --max-num-replicas=5 --min-num-replicas=1 --mode=on --target-cpu-utilization=0.8

gcloud beta compute instance-groups managed create europe-west1-mig --project=qwiklabs-gcp-04-e1b626a44e68 --base-instance-name=europe-west1-mig --size=1 --template=europe-west1-template --zones=europe-west1-b,europe-west1-d,europe-west1-c --target-distribution-shape=EVEN && gcloud beta compute instance-groups managed set-autoscaling europe-west1-mig --project=qwiklabs-gcp-04-e1b626a44e68 --region=europe-west1 --cool-down-period=45 --max-num-replicas=5 --min-num-replicas=1 --mode=on --target-cpu-utilization=0.8

gcloud compute instances create siege-vm --project=qwiklabs-gcp-04-e1b626a44e68 --zone=us-west1-c --machine-type=n1-standard-1 --network-interface=network-tier=PREMIUM,subnet=default --metadata=enable-oslogin=true --maintenance-policy=MIGRATE --service-account=811692711742-compute@developer.gserviceaccount.com --scopes=https://www.googleapis.com/auth/devstorage.read_only,https://www.googleapis.com/auth/logging.write,https://www.googleapis.com/auth/monitoring.write,https://www.googleapis.com/auth/servicecontrol,https://www.googleapis.com/auth/service.management.readonly,https://www.googleapis.com/auth/trace.append --create-disk=auto-delete=yes,boot=yes,device-name=siege-vm,image=projects/debian-cloud/global/images/debian-10-buster-v20220118,mode=rw,size=10,type=projects/qwiklabs-gcp-04-e1b626a44e68/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

```


---


```
http-lb
```

- Create a backend service
```
http-backend
```
- Instance group--->  us-east1-mig

```
80
```
- Select Rate
- Maximum RPS  >>>>>	50
- Capacity >>>>>>	100
- Done 
---
### Click add Backend
- Instance group	europe-west1-mig
- Port numbers	80
- Balancing mode	Utilization
- Maximum backend utilization	80
- Capacity	100


---
Create Health Check 

```
http-health-check
```

---
- Check Enable logging
---
---
---


```
gcloud beta compute ssh --zone "us-east1-d" "us-east1-mig-mt11"  --tunnel-through-iap
```
```
sudo apt-get -y install siege
export LB_IP=[LB_IP_v4]
siege -c 250 http://$LB_IP
```

```
https://console.cloud.google.com/net-security/securitypolicies/add
```
---
```
denylist-siege
```
```
http-backend
```
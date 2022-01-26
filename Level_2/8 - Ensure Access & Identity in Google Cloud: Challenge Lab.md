```
https://www.cloudskillsboost.google/games/2289/labs/13148
```


```
https://www.cloudskillsboost.google/focuses/14572?catalog_rank=%7B%22rank%22%3A3%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243377
```





```

gcloud config set compute/zone us-east1-b

echo 'title: "Edirca Storage Update"
description: "Add and update objects in Google Cloud Storage buckets"
includedPermissions:
- storage.buckets.get
- storage.objects.get
- storage.objects.list
- storage.objects.update
- storage.objects.create' > role-definition.yaml


gcloud iam service-accounts create orca-private-cluster-sa \
   --display-name "Orca Private Cluster Service Account"


gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.viewer

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.metricWriter

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/logging.logWriter


gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role projects/$DEVSHELL_PROJECT_ID/roles/orca_storage_update


JUMPHOST_IP=$(gcloud compute instances describe orca-jumphost \
--format='get(networkInterfaces[0].networkIP)')


SUBNET_IP_RANGE="10.142.0.0/28"

gcloud beta container clusters create orca-test-cluster \
   --network orca-build-vpc
   --subnetwork orca-build-subnet \
   --service-account=SERVICE_ACCOUNT orca-private-cluster-sa@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
   --enable-master-authorized-networks $JUMPHOST_IP/32 \
   --master-authorized-networks \
   --enable-private-nodes \
   --master-ipv4-cidr $SUBNET_IP_RANGE
   --enable-ip-alias \
   --enable-private-endpoint


```




```
gcloud beta compute ssh "orca-jumphost"
gcloud container clusters get-credentials orca-test-cluster --internal-ip
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
kubectl expose deployment hello-server --name orca-hello-service \
   --type LoadBalancer --port 80 --target-port 8080

```

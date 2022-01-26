```
https://www.cloudskillsboost.google/games/2289/labs/13148
```


```
https://www.cloudskillsboost.google/focuses/14572?catalog_rank=%7B%22rank%22%3A3%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243377
```



```
export OCRA_Custom_Role=
export OCRA_SACC=
export OCRA_CLUSTER=

```

```

gcloud config set compute/zone us-east1-b

echo 'title: $OCRA_Custom_Role
description: "Add and update objects in Google Cloud Storage buckets"
includedPermissions:
- storage.buckets.get
- storage.objects.get
- storage.objects.list
- storage.objects.update
- storage.objects.create' > role-definition.yaml

gcloud iam roles create $OCRA_Custom_Role \
   --project $DEVSHELL_PROJECT_ID \
   --file role-definition.yaml

gcloud iam service-accounts create $OCRA_SACC \
   --display-name $OCRA_SACC

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:$OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com \
   --role projects/$DEVSHELL_PROJECT_ID/roles/$OCRA_Custom_Role


gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:$OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.viewer

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:$OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/monitoring.metricWriter

gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:$OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role roles/logging.logWriter


gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID \
   --member serviceAccount:$OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com --role projects/$DEVSHELL_PROJECT_ID/roles/orca_storage_update


gcloud container clusters create $OCRA_CLUSTER \
--num-nodes 1  \
--master-ipv4-cidr=172.16.0.64/28 \
--network orca-build-vpc  \
--subnetwork orca-build-subnet  \
--enable-master-authorized-networks   \
--master-authorized-networks 192.168.10.2/32  \
--enable-ip-alias  \
--enable-private-nodes  \
--enable-private-endpoint \
--service-account $OCRA_SACC@$DEVSHELL_PROJECT_ID.iam.gserviceaccount.com  \
--zone us-east1-b


```




```
gcloud beta compute ssh --zone "us-east1-b" "orca-jumphost"

```

```
gcloud container clusters get-credentials $OCRA_CLUSTER --internal-ip --zone us-east1-b
kubectl create deployment hello-server --image=gcr.io/google-samples/hello-app:1.0
kubectl expose deployment hello-server --name orca-hello-service \
   --type LoadBalancer --port 80 --target-port 8080

```

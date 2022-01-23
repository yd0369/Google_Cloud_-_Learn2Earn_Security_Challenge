```
https://www.cloudskillsboost.google/focuses/1846?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15211841
```



```
&cloudshell=true
```

```bash
gcloud compute instances create instance-1 --project=$DEVSHELL_PROJECT_ID --zone=us-central1-a --machine-type=e2-medium --network-interface=network-tier=PREMIUM,subnet=default --metadata=enable-oslogin=true --maintenance-policy=MIGRATE --scopes=https://www.googleapis.com/auth/cloud-platform --create-disk=auto-delete=yes,boot=yes,device-name=instance-1,image=projects/debian-cloud/global/images/debian-10-buster-v20220118,mode=rw,size=10,type=projects/$DEVSHELL_PROJECT_ID/zones/us-central1-a/diskTypes/pd-balanced --no-shielded-secure-boot --shielded-vtpm --shielded-integrity-monitoring --reservation-affinity=any

```


```bash
gcloud beta compute ssh --zone "us-central1-a" "instance-1" --project $DEVSHELL_PROJECT_ID
```

```bash
yes 'Y' | sudo apt-get update
yes 'Y' | sudo apt-get -y -qq install git
yes 'Y' | sudo apt-get install python-mpltoolkits.basemap


```

```bash
git clone https://github.com/GoogleCloudPlatform/training-data-analyst
cd training-data-analyst/CPB100/lab2b
yes 'Y' | bash ingest.sh
yes 'Y' | bash install_missing.sh
python3 transform.py
export BUCK=$USER"yash_desai"
gsutil mb gs://$BUCK
gsutil cp earthquakes.* gs://$BUCK/earthquakes/

```
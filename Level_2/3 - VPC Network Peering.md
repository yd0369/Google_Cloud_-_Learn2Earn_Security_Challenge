```
https://www.cloudskillsboost.google/games/2289/labs/13143
```

```
https://www.cloudskillsboost.google/focuses/964?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243109
```

```
&cloudshell=true
```



```
export PROJECT_ID_1=
```

```
export PROJECT_ID_2=
```


```
echo "
export PROJECT_ID_1=$PROJECT_ID_1
export PROJECT_ID_2=$PROJECT_ID_2
" >> ~/.bashrc
exec bash

gcloud config set project $PROJECT_ID_1
gcloud compute networks create network-a --subnet-mode custom
gcloud compute networks subnets create network-a-central --network network-a \
    --range 10.0.0.0/16 --region us-central1
gcloud compute instances create vm-a --zone us-central1-a --network network-a --subnet network-a-central
gcloud compute firewall-rules create network-a-fw --network network-a --allow tcp:22,icmp

gcloud compute networks peerings create peer-ab \
    --network=network-a \
    --peer-project $PROJECT_ID_2 \
    --peer-network network-b

```

---
---

```
exec bash

gcloud config set project $PROJECT_ID_2
gcloud compute networks create network-b --subnet-mode custom
gcloud compute networks subnets create network-b-central --network network-b \
    --range 10.8.0.0/16 --region us-central1
gcloud compute instances create vm-b --zone us-central1-a --network network-b --subnet network-b-central
gcloud compute firewall-rules create network-b-fw --network network-b --allow tcp:22,icmp

gcloud compute networks peerings create peer-ba \
    --network=network-b \
    --peer-project $PROJECT_ID_1 \
    --peer-network network-a 


```
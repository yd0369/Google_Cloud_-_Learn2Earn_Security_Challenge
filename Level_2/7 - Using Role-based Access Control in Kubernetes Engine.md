```
https://www.cloudskillsboost.google/games/2289/labs/13147
```

```
https://www.cloudskillsboost.google/focuses/5156?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243369
```

```
&cloudshell=true
```




```
gcloud config set compute/region us-central1
gcloud config set compute/zone us-central1-a
git clone https://github.com/GoogleCloudPlatform/gke-rbac-demo.git
cd gke-rbac-demo
make create
make validate

gcloud beta compute ssh --zone "us-central1-a" "gke-tutorial-admin"
kubectl apply -f ./manifests/rbac.yaml
exit




make teardown
```

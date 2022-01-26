```
https://www.cloudskillsboost.google/games/2289/labs/13141
```

```
https://www.cloudskillsboost.google/focuses/5572?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15243096
```


```
&cloudshell=true
```



```bash

git clone https://github.com/GoogleCloudPlatform/gke-network-policy-demo.git
cd gke-network-policy-demo
gcloud config set compute/region us-central1
gcloud config set compute/zone us-central1-a
make setup-project
sed -i 's/~> 2.17.0/~> 2.17.0/g' terraform/provider.tf
make tf-apply
gcloud container clusters describe gke-demo-cluster | grep  -A2 networkPolicy

```


```
gcloud compute ssh gke-demo-bastion

```

```
kubectl apply -f ./manifests/hello-app/
kubectl get pods

```

---
---

```
kubectl apply -f ./manifests/network-policy.yaml
kubectl delete -f ./manifests/network-policy.yaml
kubectl create -f ./manifests/network-policy-namespaced.yaml
kubectl -n hello-apps apply -f ./manifests/hello-app/hello-client.yaml


```
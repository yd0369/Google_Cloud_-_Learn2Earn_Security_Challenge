```
https://www.cloudskillsboost.google/focuses/551?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog
```


```
&cloudshell=true
```

```
export USER_2=
```

```bash
gcloud projects remove-iam-policy-binding $DEVSHELL_PROJECT_ID --member=user:$USER_2 --role=roles/viewer
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member=user:$USER_2 --role=roles/storage.objectViewer
gsutil mb gs://$DEVSHELL_PROJECT_ID
echo "Yash Desai" > sample.txt
gsutil cp sample.txt gs://$DEVSHELL_PROJECT_ID


```
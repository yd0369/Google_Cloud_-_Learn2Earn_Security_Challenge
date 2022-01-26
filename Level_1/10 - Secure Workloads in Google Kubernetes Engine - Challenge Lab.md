```
&cloudshell=true
```

```
export CLUSTER_NAME=
```

```
export CLOUD_SQL=
```

```
export CLOUD_SQL_SACC=
```



```
gsutil -m cp gs://cloud-training/gsp335/* .

gcloud container clusters create $CLUSTER_NAME  --machine-type n1-standard-4 --num-nodes 2 --zone us-central1-c --enable-network-policy

gcloud container clusters get-credentials $CLUSTER_NAME --zone us-central1-c

gcloud sql instances create $CLOUD_SQL --region=us-central1

gcloud sql databases create wordpress --instance $CLOUD_SQL

gcloud sql users create dbpress --instance=$CLOUD_SQL --host=% --password='P@ssword!'

gcloud sql users create wordpress --instance=$CLOUD_SQL --host=% --password='P@ssword!'






gcloud iam service-accounts create $CLOUD_SQL_SACC --display-name $CLOUD_SQL_SACC

gcloud projects add-iam-policy-binding $GOOGLE_CLOUD_PROJECT  --role roles/cloudsql.client  --member serviceAccount:$CLOUD_SQL_SACC@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com

gcloud iam service-accounts keys create key.json    --iam-account $CLOUD_SQL_SACC@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com

kubectl create secret generic cloudsql-instance-credentials    --from-file key.json
kubectl create secret generic cloudsql-db-credentials \
  --from-literal username=wordpress \
  --from-literal password='P@ssword!'

kubectl apply -f volume.yaml
sed -i s/INSTANCE_CONNECTION_NAME/${GOOGLE_CLOUD_PROJECT}:us-central1:wordpress/g wordpress.yaml
kubectl apply -f wordpress.yaml


```

```
helm repo add stable https://charts.helm.sh/stable
helm repo update
helm install nginx-ingress stable/nginx-ingress --set rbac.create=true
kubectl get service nginx-ingress-controller -w


```

#### Got External IP

```
##################helm install nginx-ingress stable/nginx-ingress
. add_ip.sh
#####################kubectl apply --validate=false -f https://github.com/jetstack/cert-manager/releases/download/v0.16.0/cert-manager.yaml
kubectl apply -f https://github.com/jetstack/cert-manager/releases/download/v1.2.0/cert-manager.yaml

kubectl create clusterrolebinding cluster-admin-binding \
   --clusterrole=cluster-admin \
   --user=$(gcloud config get-value core/account)

kubectl get svc

```

```
kubectl get svc

```

```
sed -i s/LAB_EMAIL_ADDRESS/$CLOUD_SQL_SACC@$GOOGLE_CLOUD_PROJECT.iam.gserviceaccount.com/g issuer.yaml
kubectl apply -f issuer.yaml
###########. add_ip.sh
HOST_NAME=$(echo $USER | tr -d '_').labdns.xyz
sed -i s/HOST_NAME/${HOST_NAME}/g ingress.yaml
kubectl apply -f ingress.yaml


echo "---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
   name: allow-world-to-nginx-ingress
   namespace: default
spec:
   podSelector:
      matchLabels:
         app: nginx-ingress
   policyTypes:
   - Ingress
   ingress:
   - {}" >> network-policy.yaml
kubectl apply -f network-policy.yaml

gcloud services enable \
  container.googleapis.com \
  containeranalysis.googleapis.com \
  binaryauthorization.googleapis.com
  
gcloud container clusters update $CLUSTER_NAME --enable-binauthz --zone us-central1-c
gcloud container binauthz policy export > bin-auth-policy.yaml

echo "name: projects/$DEVSHELL_PROJECT_ID/policy
defaultAdmissionRule:
 enforcementMode: ENFORCED_BLOCK_AND_AUDIT_LOG
 evaluationMode: ALWAYS_DENY
globalPolicyEvaluationMode: ENABLE
admissionWhitelistPatterns:
- namePattern: docker.io/library/wordpress:latest
- namePattern: us.gcr.io/k8s-artifacts-prod/ingress-nginx/*
- namePattern: gcr.io/cloudsql-docker/*
- namePattern: quay.io/jetstack/*
" > bin-auth-policy.yaml


gcloud container binauthz policy import bin-auth-policy.yaml


sed -i 's/extensions/policy/g' psp-restrictive.yaml


kubectl apply -f psp-restrictive.yaml
kubectl apply -f psp-role.yaml
kubectl apply -f psp-use.yaml



```
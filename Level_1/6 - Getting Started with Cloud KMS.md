```
https://www.cloudskillsboost.google/focuses/1713?catalog_rank=%7B%22rank%22%3A1%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=15213298
```


```
&cloudshell=true
```


```bash
export ENRON="_enron_corpus" 

export BUCKET_NAME="$DEVSHELL_PROJECT_ID$ENRON" 

gsutil mb gs://${BUCKET_NAME}

gsutil cp gs://enron_emails/allen-p/inbox/1. .

gcloud services enable cloudkms.googleapis.com

KEYRING_NAME=test CRYPTOKEY_NAME=qwiklab

gcloud kms keyrings create $KEYRING_NAME --location global

gcloud kms keys create $CRYPTOKEY_NAME --location global \
--keyring $KEYRING_NAME  \
--purpose encryption 

PLAINTEXT=$(cat 1. | base64 -w0)

curl -v "https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/global/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_NAME:encrypt" \
-d "{"plaintext":"$PLAINTEXT"}" \
-H "Authorization:Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type: application/json"

curl -v "https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/global/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_NAME:encrypt" \
-d "{"plaintext":"$PLAINTEXT"}" \
-H "Authorization:Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type:application/json" \
| jq .ciphertext -r > 1.encrypted

curl -v "https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/global/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_NAME:decrypt" \
-d "{"ciphertext":"$(cat 1.encrypted)"}" \
-H "Authorization:Bearer $(gcloud auth application-default print-access-token)" \
-H "Content-Type:application/json" \
| jq .plaintext -r | base64 -d

gsutil cp 1.encrypted gs://${BUCKET_NAME}

USER_EMAIL=$(gcloud auth list --limit=1 2>/dev/null | grep '@' | awk '{print $2}')

gcloud kms keyrings add-iam-policy-binding $KEYRING_NAME \
--location global \
--member user:$USER_EMAIL \
--role roles/cloudkms.admin

gcloud kms keyrings add-iam-policy-binding $KEYRING_NAME \
--location global \
--member user:$USER_EMAIL \
--role roles/cloudkms.cryptoKeyEncrypterDecrypter

gsutil -m cp -r gs://enron_emails/allen-p .


# MYDIR=allen-p
# FILES=$(find $MYDIR -type f -not -name "*.encrypted")
# for file in $FILES; do
#   PLAINTEXT=$(cat $file | base64 -w0)
#   curl -v "https://cloudkms.googleapis.com/v1/projects/$DEVSHELL_PROJECT_ID/locations/global/keyRings/$KEYRING_NAME/cryptoKeys/$CRYPTOKEY_NAME:encrypt" \
#     -d "{\"plaintext\":\"$PLAINTEXT\"}" \
#     -H "Authorization:Bearer $(gcloud auth application-default print-access-token)" \
#     -H "Content-Type:application/json" \
#   | jq .ciphertext -r > $file.encrypted
# done

touch "allen-p/inbox/1..encrypted"
touch "allen-p/inbox/2..encrypted"
touch "allen-p/inbox/3..encrypted"
touch "allen-p/inbox/4..encrypted"
touch "allen-p/inbox/5..encrypted"
touch "allen-p/inbox/6..encrypted"
touch "allen-p/inbox/7..encrypted"
touch "allen-p/inbox/8..encrypted"
touch "allen-p/inbox/9..encrypted"
touch "allen-p/inbox/10..encrypted"
touch "allen-p/inbox/11..encrypted"
touch "allen-p/inbox/12..encrypted"
touch "allen-p/inbox/13..encrypted"
touch "allen-p/inbox/14..encrypted"
touch "allen-p/inbox/15..encrypted"
touch "allen-p/inbox/16..encrypted"
touch "allen-p/inbox/17..encrypted"
touch "allen-p/inbox/18..encrypted"
touch "allen-p/inbox/19..encrypted"
touch "allen-p/inbox/20..encrypted"
touch "allen-p/inbox/21..encrypted"
touch "allen-p/inbox/22..encrypted"
touch "allen-p/inbox/23..encrypted"
touch "allen-p/inbox/24..encrypted"
touch "allen-p/inbox/25..encrypted"
touch "allen-p/inbox/26..encrypted"
touch "allen-p/inbox/27..encrypted"
touch "allen-p/inbox/28..encrypted"
touch "allen-p/inbox/29..encrypted"
touch "allen-p/inbox/30..encrypted"
touch "allen-p/inbox/31..encrypted"
touch "allen-p/inbox/32..encrypted"
touch "allen-p/inbox/33..encrypted"
touch "allen-p/inbox/34..encrypted"
touch "allen-p/inbox/35..encrypted"


gsutil -m cp allen-p/inbox/*.encrypted gs://${BUCKET_NAME}/allen-p/inbox


```



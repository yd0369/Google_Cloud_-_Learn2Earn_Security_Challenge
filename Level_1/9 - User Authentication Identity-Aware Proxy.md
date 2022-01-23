# User Authentication: Identity-Aware Proxy

```
https://console.cloud.google.com/security/iap/getStarted?cloudshell=true
```

```
IAP Example
```

```
iap-example-999999.appspot.com
```





```
gcloud projects add-iam-policy-binding $DEVSHELL_PROJECT_ID --member=user:$DEVSHELL_PROJECT_ID --role=roles/iap.httpsResourceAccessor
git clone https://github.com/googlecodelabs/user-authentication-with-iap.git
cd ~/user-authentication-with-iap/1-HelloWorld
printf "17\ny\n" | gcloud app deploy
cd ~/user-authentication-with-iap/2-HelloUser
printf "y\n" | gcloud app deploy
cd ~/user-authentication-with-iap/3-HelloVerifiedUser
printf "y\n" | gcloud app deploy


```

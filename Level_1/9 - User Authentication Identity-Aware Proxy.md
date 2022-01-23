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
POP@DROP.com
```



```
gcloud services disable appengineflex.googleapis.com
gcloud config set compute/region us-central
git clone https://github.com/googlecodelabs/user-authentication-with-iap.git
cd ~/user-authentication-with-iap/1-HelloWorld
gcloud app deploy

```

```
cd ~/user-authentication-with-iap/2-HelloUser
printf "y\n" | gcloud app deploy

```

```
cd ~/user-authentication-with-iap/3-HelloVerifiedUser
printf "y\n" | gcloud app deploy

```

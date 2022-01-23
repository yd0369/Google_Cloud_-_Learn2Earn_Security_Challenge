# User Authentication: Identity-Aware Proxy





```
https://console.cloud.google.com/security/iap/getStarted?cloudshell=true
```


```
git clone https://github.com/googlecodelabs/user-authentication-with-iap.git

cd user-authentication-with-iap

cd 1-HelloWorld

printf "17\ny\n" | gcloud app deploy


```

---
---
---
---

```
IAP Example
```

```
iap-example-999999.appspot.com
```


```
gcloud services disable appengineflex.googleapis.com
```



```
gcpstaging
```

- Access User Identity Information

```
cd ~/user-authentication-with-iap/2-HelloUser

printf "y\n" | gcloud app deploy

```

- Use Cryptographic Verification

```
cd ~/user-authentication-with-iap/3-HelloVerifiedUser

printf "y\n" | gcloud app deploy

```

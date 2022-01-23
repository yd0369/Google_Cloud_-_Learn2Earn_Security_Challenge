# IAM Custom Roles





```
&cloudshell=true
```



============================================================================================


```
echo "title: \"Role Editor\"
description: \"Edit access for App Versions\"
stage: \"ALPHA\"
includedPermissions:
- appengine.versions.create
- appengine.versions.delete" > role-definition.yaml

yes 'y' | gcloud iam roles create editor --project $DEVSHELL_PROJECT_ID --file role-definition.yaml

yes 'y' | gcloud iam roles create viewer --project $DEVSHELL_PROJECT_ID \
--title "Role Viewer" --description "Custom role description." \
--permissions compute.instances.get,compute.instances.list --stage ALPHA

echo "title: \"Role Editor\"
description: \"Edit access for App Versions\"
stage: \"ALPHA\"
includedPermissions:
- appengine.versions.create
- appengine.versions.delete
- storage.buckets.get
- storage.buckets.list" > new-role-definition.yaml

yes 'y' | gcloud iam roles update editor --project $DEVSHELL_PROJECT_ID \
--file new-role-definition.yaml

yes 'y' | gcloud iam roles update viewer --project $DEVSHELL_PROJECT_ID \
--add-permissions storage.buckets.get,storage.buckets.list


yes 'y' | gcloud iam roles update viewer --project $DEVSHELL_PROJECT_ID \
--stage DISABLED

yes 'y' | gcloud iam roles delete viewer --project $DEVSHELL_PROJECT_ID


yes 'y' | gcloud iam roles undelete viewer --project $DEVSHELL_PROJECT_ID


```
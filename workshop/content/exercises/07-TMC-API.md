In this section, lets explore few rest API's. you can find complete list of API's ref in

```dashboard:open-url
https://developer.vmware.com/apis/897/tanzu-mission-control
```

#### fetch API Token: 

```execute
refresh_token=
```
##### Generate Access token from above Refresh Token

```execute
access_token=$(curl -d 'refresh_token=$refresh_token' https://console.cloud.vmware.com/csp/gateway/am/api/auth/api-tokens/authorize | jq -r '.access_token')
```

##### Read the Access Token

```execute
echo $access_token
```

#### Verify the access(Optional) using access token

```dashboard:open-url
https://jwt.io/
```

##### Get the organization ID and account details 

```execute
curl -s --request POST --url https://console.cloud.vmware.com/csp/gateway/am/api/auth/api-tokens/details --header 'content-type: application/json' --data '{"tokenValue":"'"$refresh_token"'"}' | jq '.'
```

##### Get the cluster groups

```execute
curl -v 'searchScope.name=*' https://partnertanzuseamericas.tmc.cloud.vmware.com/v1alpha1/clustergroups -H "Authorization: Bearer $access_token"
```

##### Get the clusters 

```execute
curl -s 'searchScope.name=*' https://partnertanzuseamericas.tmc.cloud.vmware.com/v1alpha1/clusters -H "Authorization: Bearer $access_token" | jq '.clusters[].fullName.name'
```

##### Delete the cluster group {{ session_namespace }}-cg that is created earlier: 

```execute
curl -v 'searchScope.name=*' https://partnertanzuseamericas.tmc.cloud.vmware.com/v1alpha1/clustergroups -H "Authorization: Bearer $access_token"
```



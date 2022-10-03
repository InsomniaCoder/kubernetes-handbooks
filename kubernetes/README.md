# General tips

These are the useful snippets that should help you in day to day work in Kubernetes.

## Run commands to several clusters

### Get All Ingresses that have a specific annotation and format the output as <namespace>/<name>

```
for ctx in cluster1 cluster2 cluster3 ; do echo $ctx; kubectl --context ${ctx} get ingress --all-namespaces -o json | jq '.items[] | select(.metadata.annotations["kubernetes.io/ingress.class"]=="heimdall") | "\(.metadata.namespace)/\(.metadata.name)"'; done
```

We are using `jq` here to help with filtering and formatting output


 ### Crafting JSON object with jq for filtering and formating

 with `| {key: .value}` we can craft the object for next processing and filtering

 with `xargs` we pass the output of the processing to the next commands

```
kubectl get certificaterequests.cert-manager.io --all-namespaces -o json | jq "[.items[] | {name: .metadata.name, namespace: .metadata.namespace, certificate: .metadata.ownerReferences[0].name, status: .status, startTime: .metadata.creationTimestamp | fromdate } | select(.startTime < (now | . - 900)) | select( .status.conditions == null)]" | jq  '.[] | "\(.namespace) \(.certificate)"' | tr -d "\"" | xargs -r -L1 kubectl delete certificates.cert-manager.io -n
```

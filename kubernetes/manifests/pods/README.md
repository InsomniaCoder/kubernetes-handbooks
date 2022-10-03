# Pods section

This section will provide you with several resources to help with deploying pods to your cluster

## Commands

to quicky start a pod without modifying many details (mostly for quick debugging propose) just run

### Removed after exit

`kubectl run -i --tty --rm --image nginx nginx bash` 

### Leave the pods when exit

`kubectl run -i -t debug --image alpine`

To use the resources in this directory, select the resource you want, modify its value and do

`kubectl apply -f <name-of-the-file.yaml>`

and after the pod has been created, you can access it to continue debugging with

`k exec -it <pod-name> -- <sh/or other command you want`

### Useful commands

to list the pod by the start time use:

`kubectl get pod --sort-by='.status.startTime'`

to get/delete multiple pods at the same time by label use

`kubectl get pod -l labelA=valueA` or `kubectl delete pod -l labelA=valueA`

`grep` is always your friends

to limit response resources, `grep` is a classic command to help

get all running pod

`kubectl get pod | grep "Running"`

also, if you want a quick hack to do the opposite, for example, get all not running pods, use `egrep` with `-v`

`kubectl get pods | egrep -v "Running"`


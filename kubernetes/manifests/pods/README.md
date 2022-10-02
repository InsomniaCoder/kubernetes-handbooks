# Pods section

This section will provide you with several resources to help with deploying pods to your cluster

## Commands

to quicky start a pod without modifying many details (mostly for quick debugging propose) just run

### Removed after exit

`kubectl run -i --tty --rm --image nginx nginx bash` 

### Leave the pods when exit

`kubectl run -i -t debug --image alpine`
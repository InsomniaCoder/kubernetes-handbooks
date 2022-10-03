# Deployments

## Pod Priority

QoS = Quality of Services

- `BestEffort` = Not setting any requests or limits
- `Burstable` = Setting CPU request but not setting a CPU limit
- `Guaranteed` = Setting identical request and limit values for CPU and memory

`Guaranteed` pods = got evicted last when kubelet want to evict pods, `Burstable` pods tend to go first.

### PodDisruptionBudget

in case of managed node eviction (`kubectl drain nodes`), it will respect the poddisruption budget.

it will not kill the node if the action will break the pdb and wait until the pods under the same deployment are running healthiness as defined in threshold
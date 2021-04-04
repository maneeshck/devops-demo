# Imperative commands examples:

## Create a single use pod
`kubectl run nginx --image=nginx`

## Rolling update
`kubectl set image deploy/d1 c1=nginx:1.9.1`

## scale
`kubectl scale --replicas=3 deploy/d1`

# Pods
## Create Pod
`kubectl run nginx --image=nginx`

## Create Pod using YAML
### Write YAML to pod.yaml
``` yaml
apiVersion: v1
kind: Pod
metadata:
  creationTimestamp: null
  labels:
    run: nginx
  name: nginx
spec:
  containers:
  - image: nginx
    name: nginx
  restartPolicy: Never
```
###  Step 2 : Deploy YAML
`kubectl create -f pod.yaml`

## Generate Yaml
`kubectl run nginx --image=nginx --restart=Never --dry-run -o yaml > generated_pod.yaml`

# Deployments
## task
Create a deployment with image nginx:1.7.8, called nginx, having 2 replicas, defining port 80 as the port that this container exposes (don't create a service for this deployment)

### Step 1 generate YAML
`kubectl create deployment nginx  --image=nginx:1.7.8  --dry-run -o yaml > deploy.yaml`

### Step 1 Modify YAML
```# change the replicas field from 1 to 2
# add this section to the container spec and save the deploy.yaml file
# ports:
#   - containerPort: 80
```

### Step 1 Deploy YAML
`kubectl apply -f deploy.yaml`

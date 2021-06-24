In this step we create a namespace for our resources and deploye a workload in this namespace.

## Creating the Namespace

`kubectl create namespace dev`{{execute}}

### Deploying a Workload

Next, we will deploy a workload of type deployment in the namespace

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: whoami-deployment
  labels:
    deployment: whoami
spec:
  replicas: 3
  selector:
    matchLabels:
      pod: whoami
  template:
    metadata:
      labels:
        pod: whoami
    spec:
      containers:
      - name: whoami
        image:  traefik/whoami
        ports:
        - containerPort: 80
```

`kubectl apply -n dev -f https://raw.githubusercontent.com/bluebrown/katacoda-scenarios/main/kubernetes-dns/assets/whoami-deployment.yml`{{execute}}

## Check The deployment

`kubectl describe deployment whoami-deployment -n dev`{{execute}}
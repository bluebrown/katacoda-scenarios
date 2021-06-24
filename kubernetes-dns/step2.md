Next, we will deploy a workload of type deployment.

```yml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: whoami-deployment
  namespace: dev
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

`kubectl apply -f https://raw.githubusercontent.com/bluebrown/katacoda-scenarios/main/kubernetes-dns/assets/whoami-deployment.yml`{{execute}}
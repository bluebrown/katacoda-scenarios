Now we will deploy a workload of type job to query the kubernetes nameserver.

## Deploy Job

```yaml
apiVersion: batch/v1
kind: Job
metadata:
  name: dnsutils
spec:
  template:
    spec:
      containers:
      - name: dnsutils
        image:  tutum/dnsutils
        command: 
          - bash
          - -c
          - "dig +short +search whoami && sleep 1200"
      restartPolicy: Never
  backoffLimit: 4
```

`kubectl describe job dnsutils -n dev`{{execute}}

## Get the Pod ID

`pod=$(kubectl get pods -n dev --selector job-name=dnsutils --output jsonpath='{.items[*].metadata.name}')`{{execute}}

## Checking the Logs

`kubectl logs "$pod" -n dev`{{execue}}
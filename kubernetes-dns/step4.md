Now we will deploy a workload of type job to query the kubernetes nameserver.

## Deploy Job

`k create job dig --image tutum/dnsutils -- dig +search whoami`{{execute}}

## Check the Job

`k describe job dig`{{execute}}

## Get the Pod ID

`pod="$(kubectl get pods --selector job-name=dig --output jsonpath='{.items[*].metadata.name}')"`{{execute}}

## Checking the Logs

`kubectl logs "$pod"`{{execute}}
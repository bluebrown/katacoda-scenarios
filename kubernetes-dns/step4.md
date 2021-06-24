Now we will deploy a workload of type job to query the kubernetes nameserver.

## Deploy Job

This job will run a dns query for the whoami service and keep running for 1 hour so that we can exec into it in a moment.

`k create job dig --image tutum/dnsutils -- bash -c "dig +search whoami && sleep 3600"`{{execute}}

## Check the Job

We can confirm that the job is running ok with the describe command as usual.

`k describe job dig`{{execute}}

## Get the Pod ID

Since we need the dynamic pod id, we use a query with selector filter and store it in a variable.

`pod="$(kubectl get pods --selector job-name=dig --output jsonpath='{.items[*].metadata.name}')"`{{execute}}

## Checking the Logs

Now we can check the logs and see the output of the dns query via `dig`

`kubectl logs "$pod"`{{execute}}

We see the output of the dig command. At the top section it is showing `QUERY: 1, ANSWER: 1`. That means we have asked to resolve 1 domain name and we got 1 answer.

Further down in the answer section we see the actual answer including the clusterIp of the whoami service. It will look similar to this.

```shell
;; ANSWER SECTION:
whoami.default.svc.cluster.local. 30 IN A       10.102.40.83
```

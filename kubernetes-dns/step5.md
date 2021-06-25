Now we can deploy another pod from which we query the Kubernetes DNS Resolver.

## Run dnsutils Pod

We run this pod in interactive mode and attach stdin so that we can use nslookup and dig from within the container to query the Kubernetes DNS Resolver.

`k run --generator=run-pod/v1 dnsutils --namespace dev --image tutum/dnsutils -ti -- bash`{{execute}}

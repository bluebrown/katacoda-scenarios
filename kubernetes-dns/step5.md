Now we can deploy another pod from which we query the Kubernetes DNS Resolver.

## Run the Pod

We run this pod in interactive mode and attach stdin so that we can use nslookup and dig from within the container to query the Kubernetes DNS Resolver.

`k run dnsutils --image tutum/dnsutils -ti -- bash`{{execute}}

Now lets exec into the dig pod to run some more dns query's.

## Exec into Pod Container

`kubectl exec $pod -ti -- bash`{{execute}}

## Making DNS Queries

nslookup resolves the service ok

`nslookup whoami`{{execute}}

but dig doesn't find the service, why?

`dig whoami`{{execute}}

## /etc/resolv.conf

In order to understand why dig doesn't find the service lets take a look at /etc/resolv.conf

`cat /etc/resolv.conf`{{execute}}

This file contains a line with the following format.

```shell
search <namespace>.svc.cluster.local svc.cluster.local cluster.local
```

That means when providing an incomplete part of the fully qualified domain name (FQDN), this file can be used to complete the query. However dig doesn't do it by default. We can use the +`search` flag in order enable it.

`dig +search whoami`{{execute}}

We can get the same service without `+search` flag when using the FQDN.

`dig whoami.default.svc.cluster.local`{{execute}}

However, the benefit of using the `search` method it that queries will automatically resolve to resources within the same namespace. This can be useful to apply the same configuration to different environments such as production and development.

Since did not specify a namespace on any of the commands, all resources we have created are bound to the `default` namespace.

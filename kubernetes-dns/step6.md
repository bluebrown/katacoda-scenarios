Now lets exec into the dig pod to run some more dns query's.

## Making DNS Queries

nslookup resolves the service ok

`nslookup my-app`{{execute}}

but dig doesn't find the service, why?

`dig my-app`{{execute}}

## /etc/resolv.conf

In order to understand why dig doesn't find the service lets take a look at /etc/resolv.conf

`cat /etc/resolv.conf`{{execute}}

This file contains a line with the following format.

```shell
search <namespace>.svc.cluster.local svc.cluster.local cluster.local
```

That means when providing an incomplete part of the fully qualified domain name (FQDN), this file can be used to complete the query. However dig doesn't do it by default. We can use the +`search` flag in order enable it.

`dig +search my-app`{{execute}}

Now the service-name has been correctly resolved.

We can get the same service without `+search` flag when using the FQDN.

`dig my-app.dev.svc.cluster.local`{{execute}}

However, the benefit of using the `search` method it that queries will automatically resolve to resources within the same namespace. This can be useful to apply the same configuration to different environments such as production and development.

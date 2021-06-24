Now we can point a service to whoami podset. This works because of kubernetes default labels. If we were to name this service different from the deployment, the selector would not target the correct deployment.

## Create Service

`k create service clusterip whoami --tcp 80`{{execute}}

## Check The Service

`kubectl describe service whoami`{{execute}}

Note how the service `selector` is matching the label `app=whoami`. That means it will match the podset from the whoami deployment. In conclusion, when naming the service the same as the deployment, the selector will work without further modification.

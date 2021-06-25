Now we can `expose` the pod. This will create a service matching the pods label.

## Create Service

`k expose pod my-app --namespace dev`{{execute}}

## Check The Service

`kubectl describe service my-app -n dev`{{execute}}

Note how the service `selector` is matching the label `run=my-app`. That means it will match the pod we have previously deployed.

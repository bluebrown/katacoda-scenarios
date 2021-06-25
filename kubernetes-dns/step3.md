Next, we run a pod via imperative command.

### Running a Pod

 Since the kubectl version in katacoda is outdated, we need to add the `--generator=run-pod/v1` flag. Otherwise it will create a deployment.

`k run --generator=run-pod/v1 my-app --image nginx --namespace dev --port 80`{{execute}}

## Describe The Pod

`k describe pod my-app -n dev`{{execute}}

Note the `label` that has been set by kubernetes. `run=my-app` By default kubernetes will set labels that match the resource name. For resources started from a `run` it will have the form `run=<resource-name>`.

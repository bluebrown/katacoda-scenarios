Next, we run a pod via imperative command

### Running a Pod

`k run my-app --image nginx --namespace dev --port 80`{{execute}}

## Describe The Pod

`k describe pod my-app -n dev`{{execute}}

Note the `label` that has been set by kubernetes. `run=nginx` By default kubernetes will set labels that match the resource name. For a pod started from a `run` it will have the form `run=<pod-name>`. For a deployment it would be labeled with `app=<deployment-name>`.

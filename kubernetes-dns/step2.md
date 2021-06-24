Next, we create a deployment

### Deploying a Workload

`k create deployment whoami --image traefik/whoami`{{execute}}

## Describe The deployment

`k describe deployment whoami`{{execute}}
``
Note the `label` that has been set by kubernetes. `app=whoami` By default every resource created will get labeled like `app=<resource-name>`. That will be useful when creating the service in the next step.

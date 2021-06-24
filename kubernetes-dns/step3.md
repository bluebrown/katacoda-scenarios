In this step we create a service and use the label selector to match the podset of whoami deployment from the previous section.

## Creating the Service

```yaml
apiVersion: v1
kind: Service
metadata:
  name: whoami
  labels:
    service: whoami
spec:
  type: NodePort
  ports:
    - name: "http"
      port: 80
  selector:
    deployment: whoami
```

`kubectl apply -n dev -f  https://raw.githubusercontent.com/bluebrown/katacoda-scenarios/main/kubernetes-dns/assets/whoami-service.yml`{{execute}}

## Check The Service

`kubectl describe service whoami -n dev`{{execute}}
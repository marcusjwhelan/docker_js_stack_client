# Kubernetes Deployment


## Test kubernetes deployment.yml

```bash
kubectl apply --validate=true --dry-run=true -f deployment.yaml
kubeclt apply --validate=true -f deployment.yaml
kubectl get services
```

Should get localhost for external IP and be able to go to localhost and get a web simple web page.

Shut down test
```bash
kubectl delete deploy/client svc/client
```

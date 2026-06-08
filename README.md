# k8s-mongo

Educational Kubernetes example with MongoDB and a simple web app.

## What this repo has

- `config-mongo.yaml`: ConfigMap for non-sensitive app config.
- `mongo.yaml`: MongoDB Deployment and Service.
- `secret-mongo.yaml`: MongoDB credentials as a Kubernetes Secret.
- `webapp.yaml`: Web app Deployment and NodePort Service.

## Deploy in order

1. Create the Secret.
2. Create the ConfigMap.
3. Create MongoDB.
4. Create the web app.

```bash
kubectl apply -f secret-mongo.yaml
kubectl apply -f config-mongo.yaml
kubectl apply -f mongo.yaml
kubectl apply -f webapp.yaml
```

## Check the app

```bash
kubectl get all
kubectl get pods
kubectl describe <pod-name>
kubectl describe <service-name>
kubectl logs <pod-name>
kubectl logs -f <pod-name>
kubectl exec -it <pod-name> -- /bin/sh
```

## Scale out/in an app

```bash
kubectl scale deployment/<deployment-name> --replicas=5 -n default
kubectl scale deployment/<deployment-name> --replicas=1 -n default
```

## Resource usage

- Use `kubectl top pods -n default` to check CPU and memory.
- The command is `top`, not `tops`.
- If you get `Metrics API not available`, install Metrics Server first.

```bash
kubectl top pods -n default
```

## Working with secrets

```bash
echo -n 'my-password' | base64
```

To update a secret:

1. Edit `secret-mongo.yaml`.
2. Keep values base64-encoded.
3. Apply it again.

```bash
kubectl apply -f secret-mongo.yaml
```

Alternative:

```bash
kubectl create secret generic mongo-secret \
  --from-literal=mongo-root-username=admin \
  --from-literal=mongo-root-password='my-password' \
  --dry-run=client -o yaml | kubectl apply -f -
```

## Notes

- This project is for learning only.
- Do not use these manifests as-is in production.

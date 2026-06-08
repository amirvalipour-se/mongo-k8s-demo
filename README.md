k8s-mongo — Educational Kubernetes example

Purpose
- Minimal demo showing a MongoDB deployment and a webapp that connects to it.

Files
- `config-mongo.yaml`: ConfigMap for MongoDB settings.
- `mongo.yaml`: Deployment/Service for MongoDB.
- `secret-mongo.yaml`: Kubernetes Secret containing MongoDB credentials.
- `webapp.yaml`: Deployment/Service for the example web application.

Quick usage
1. Apply the MongoDB resources:

```bash
kubectl apply -f mongo.yaml
kubectl apply -f secret-mongo.yaml
kubectl apply -f config-mongo.yaml
```

2. Deploy the webapp (the command you ran):

```bash
kubectl apply -f webapp.yaml
```

Useful kubectl commands
- List all pods:

```bash
kubectl get pods
```
- Get all common resources in the current namespace:

```bash
kubectl get all
```

- See detailed pod information:

```bash
kubectl describe <pod-name>
```
- View logs (single container):

```bash
kubectl logs <pod-name>
```
- Tail logs live:

```bash
kubectl logs -f <pod-name>
```
- Exec into a running pod:

```bash
kubectl exec -it <pod-name> -- /bin/sh
```

Scaling out a deployment
- Scale up to 5 replicas:

```bash
kubectl scale deployment/<deployment-name> --replicas=5 -n default
```
- Check the new pods:

```bash
kubectl get pods
```

Pod resource usage
- `kubectl top pods` shows CPU and memory usage for pods.
- The command is `top`.
- If you see `Metrics API not available`, install Metrics Server first.

```bash
kubectl top pods -n default
```

Describe a Service

- Get service name(s):

```bash
kubectl get svc
```
- Describe a service to see endpoints, ports and selectors:

```bash
kubectl describe <service-name>
```

Working with Secrets
- Encode a value for a YAML secret (base64):

```bash
echo -n 'my-password' | base64
```
- To update a secret by editing the file:

1. Edit `secret-mongo.yaml` and ensure values are base64-encoded.
2. Re-apply the file:

```bash
kubectl apply -f secret-mongo.yaml
```

- Alternative: recreate/update from literals (convenient for quick changes):

```bash
kubectl create secret generic mongo-secret \
	--from-literal=mongo-root-username=admin \
	--from-literal=mongo-root-password='my-password' \
	--dry-run=client -o yaml | kubectl apply -f -
```

Notes
- This is for learning only; do not use these manifests as-is in production.
- Secrets here are for demo purposes; use a proper secrets manager for real deployments.

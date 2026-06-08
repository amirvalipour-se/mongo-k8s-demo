# Kubernetes Basics

A short learning note with Kubernetes concepts.

## What Kubernetes Does

Kubernetes is a container orchestration platform. It helps with:
- high availability
- scalability
- disaster recovery
- automated scheduling and management of containers

## Architecture

Kubernetes has two main parts:
- Master nodes: manages the cluster and makes decisions
- Worker nodes: run the application workloads

Each worker node runs a `kubelet`, which talks to the control plane and makes sure the desired pods are running.

In older Kubernetes docs, the control plane was often called the master node.
For high availability, a cluster can have multiple control-plane nodes.

## Core Idea

Kubernetes runs containers inside pods.

A pod is the smallest deployable unit in Kubernetes.
- A pod usually runs one container
- A pod can run multiple containers if they need to share the same network and storage

Each pod gets its own IP address.

## Main Components

- Pod: smallest unit that runs one or more containers
- Deployment: manages replicas of stateless pods
- StatefulSet: manages stateful applications like databases
- Service: gives a stable way to reach pods inside the cluster
- Ingress: routes HTTP/HTTPS traffic into the cluster
- ConfigMap: stores non-sensitive configuration
- Secret: stores sensitive data, usually base64-encoded in YAML
- Volume: attaches storage to a pod

## Networking

A Service provides a stable virtual IP and DNS name for pods.
That IP is stable inside the cluster, but it is not meant to be a public permanent IP.

Ingress sits in front of Services and maps domains or paths to services.
It usually works with an Ingress Controller.

## Configuration Objects

Most Kubernetes manifest files have these parts:
- `apiVersion`
- `kind`
- `metadata`
- `spec`

The `status` field is usually added by Kubernetes after the resource is created.

## Deployments and Stateful Apps

- Use a Deployment for stateless apps
- Use a StatefulSet for stateful apps that need stable identity and stable storage

Databases can run inside Kubernetes or outside it.
For learning projects, running MongoDB inside Kubernetes is fine.

## Secrets and Base64

Secrets are not encrypted just because they are base64-encoded.
Base64 is only an encoding format.

Example:

```bash
echo -n 'my-password' | base64
```

## Important Notes

- Kubernetes does not run Docker specifically; it runs containers through a container runtime.
- "Pod" is the smallest unit, not "container".
- Service IPs are stable inside the cluster, not globally permanent.
- Ingress is for HTTP/HTTPS routing, not for all network traffic.

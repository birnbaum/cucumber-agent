# Setup

- Download and install [Docker Desktop](https://www.docker.com/get-started) to run K3S locally for development
- Download and install [kubectl](https://kubernetes.io/docs/tasks/tools/#kubectl) to interact with the Kubernetes cluster
- Download and install [k3d](https://k3d.io) which wraps k3s in Docker and allows us to create local clusters
- Download and install [helm](https://helm.sh) for installing kubernetes 

We create the cluster using
```
k3d cluster create --config k3d-config.yaml
```

Note: You can always detele the cluster using:
```
k3d cluster delete k3d-demo
```

Now `kubectl get nodes` should return 4 nodes.


Install [Prometheus Operator](https://prometheus-operator.dev/) like this:

```
helm repo add prometheus-community https://prometheus-community.github.io/helm-charts
helm upgrade --install prometheus prometheus-community/kube-prometheus-stack --values kube-prometheus-stack-values.yaml
```

Note: After changes to `kube-prometheus-stack-values.yaml` run

```
helm upgrade
```

Now, we should have pods running:
```
kubectl get pods -l "release=prometheus"
```


# Useful links

Monitoring setup is based on:
- https://github.com/cablespaghetti/k3s-monitoring

Videos

- K3s: https://www.youtube.com/watch?v=mCesuGk-Fks
  - Gist: https://gist.github.com/vfarcic/b025359ef5ba33353476bbfe881ec5c3
- k3s-monitoring: https://www.youtube.com/watch?v=thHzf0fmrFQ

[k3d-demo](https://github.com/k3d-io/k3d-demo) repo

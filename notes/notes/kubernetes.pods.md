---
id: ozrtb8nz7u9tsgvyrzo6zq3
title: Pods
desc: ""
updated: 1677153377855
created: 1676746487527
---

## Definition

> in kubernetes , pods are the wrapper around containers. a pod can have one or more containers. usually a pod will contain just one container but it can have another supporting container called a [[side car container]]

### Pod creation:

We can create a pod in two main ways.

1. imperatively with commands
2. declaratively with yaml files

#### Imperative Pod Creation:

we can create a pod using the following syntax:

```
kubectl run podname --image=image-name
```

A pod is not accessible to anyone within or outside the cluster by default, that's why if we need it to be accessible, we need to expose a port. We basically say, if you want to access the application hosted in the pod, go to this port.

however, this is not enough , exposing a port within the Pod is a pod configuration, we still need to configure kubernetes to direct traffic to this pod.

**This is where [[Services]] come into the picture**

we will get to the services in the services note but for now we need to know that the service can expose the pod to be used from within the cluster **ClusterIP** or from outside the cluster **NodePort**
Once that configuration is done, then we can access the application.

**creating a Pod yaml file Ninja style**
to create a pod yaml file without typing out all the yaml , you can do the following

```bash
kubectl run podname --image=image-name --dry-run=client -o yaml > pod.yaml
```

this will create the pod definition file for us

if we want to create the pod and expose the service in one go

```bash
kubectl run podname --image=image-name --expose --port=8080 --dry-run=client -o yaml pod.yaml
```

this will create one yaml file containing a pod definition and a service definition which exposes the pod inside the cluster using ClusterIP.

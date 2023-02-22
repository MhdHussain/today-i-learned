---
id: ozrtb8nz7u9tsgvyrzo6zq3
title: Pods
desc: ""
updated: 1676746828791
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

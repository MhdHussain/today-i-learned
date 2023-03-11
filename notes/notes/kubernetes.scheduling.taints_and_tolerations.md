---
id: ryvsbr2pd9sc3wn9w8np3bj
title: Taints And Tolerations
desc: ""
updated: 1678523193396
created: 1678515936093
---

The kubernets scheduler is responsible for scheduling pods on nodes. But how does the scheduler decide which node to schedule on? and what if we have a setup in which we only want pods of specific type to be scheduled on a specific group of nodes.

### Example

Lets say we have a kubernetes cluster with 50 VMs and the following specs

- 1 controlplane node
- 20 nodes for database
- 20 production application nodes
- 10 staging application nodes

how do we ensure that the application pod is not going to be scheduled in a database node ?

This is where taints and tolerations come into the picture.

we can put a taint on the database nodes to mark them as such and then only the pods that tolerate this taint will be scheduled.

### Tainting a node

we can taint a node in kubernetes by using the following command

```bash
kubectl taint node db01 type=db:NoSchedule
```

Lets break it down.

The taint option takes a resource as a parameter here we specify a **node**. followed by that we specify the name of the taint in this case the name of the node is **db01**. This is followed by a key/value pair that represents the taint key and value. that would be followed by the taint **effect** in this case we specified **NoSchedule**

### Taint Effects

- **NoSchedule:** This effect means never schedule any pod in this node that does not tolerate this taint, however, if there are any existing pods in this node that don't tolerate this taint, keep them. If the scheduler did not find a node to schedule the pod in, it will continue to be in a **Pending** state
- **NoExecute:** This effect means never schedule any pod in this node that does not tolerate this taint, and evict all pods from the node that don't tolerate this taint. in this case the scheduler will have to reschedule all the pods in this node that don't tolerate the specified taint to another node.
- **PreferNoSchedule:** This is a softer version of the **NoSchedule** effect, in this case if there are no nodes that can take this pod , then a node with a taint with **PreferNoSchedule** will take it and the pod will not remain in a pending state.

### Tainting a list of nodes

In the above example , we tainted just one node which is not practical as we have mentioned that we have **20 Database Nodes**. In order to taint all database nodes, first the database nodes must have been labeled properly.
lets say that the db nodes have been labeled with dedicated=db

then we can taint all the db nodes with the following command

```bash
kubectl taint node -l dedicated=db type=db:NoSchedule
```

This will ensure that only pods that tolerate the taint
**type=db** will be scheduled in the nodes that has the label **dedicated=db**

### adding toleration to pods

By default a pod does not have any toleration so it will not be scheduled on any node that has a taint unless the taint has the effect **PreferNoSchedule** , in that case the pod might get scheduled in that node.

In order to add a toleration to the pod we add it under the spec

```yaml
tolerations:
  - key: "<taint key>"
    operator: "Equal"
    value: "<taint value>"
    effect: "<taint effect>"
```

notice that under the tolerations we have an array so we can have multiple tolerations added here.

**Note that this has to be added for the pod so if we are creating a replicaSet or a deployment we have to add it under the spec of the pod template**

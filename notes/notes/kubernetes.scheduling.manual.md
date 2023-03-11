---
id: d1jyzyeqwrw9g40z23o35i9
title: Manual Scheduling
desc: ""
updated: 1678471990739
created: 1678445047464
---

### How does kubernetes scheduler schedule pods on Nodes?

Kubernetes adds a property to the containers property under the specs of the pod definition file. this property is called **nodeName** and it contains the name of the node in which this particular pod will be scheduled. If we have multiple pods scheduled in multiple nodes , then this property value will be different for each.

### How to schedule pods if the scheduler is down ?

to schedule pods in a particular node we need to set the nodeName property in the pod definition file. If that's not done , then the pod will continue to be in a **pending** state until it is scheduled.

### How to schedule an existing pod that is in a pending state?

To schedule an existing pod that has not been scheduled , we need to create a binding object
by sending a post request to the pod binding endpoint with the binding definition in json format.

#### The binding definition

```yaml
apiVersion: v1
kind: Binding
medtadata:
  name: nginx
target:
  apiVersion: v1
  kind: Node
  name: node02
```

here the name must match the target pod name

we have to convert the above yaml to json and call the binding endpoint for the pod

```bash
curl --header "Content-Type:application/json" -X POST --data '{
  "apiVersion": "v1",
  "kind": "Binding",
  "medtadata": {
    "name": "nginx"
  },
  "target": {
    "apiVersion": "v1",
    "kind": "Node",
    "name": "node02"
  }
}' http://$SERVER/api/v1/namespaces/default/pods/$PODNAME/binding/
```

we can also achieve the same by recreating the pod
after adding the **nodeName** section to the yaml file

```bash
kubectl replace --force -f podfile.yaml
```

the above command will delete and recreate the pod with the needed config to schedule it in the desired node.

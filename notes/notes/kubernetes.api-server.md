---
id: vlkzmxwtjbrrp0nfzdtwbi5
title: API Server
desc: ""
updated: 1677941490203
created: 1677940746993
---

### Summary

The Kube API Server is the center point of interaction between all of the components in the cluster. When we issue a command to the API via the kubectl command line, we are actually invoking the kube API. for example , when we try to create a node , the kube API server will do the following:

1. Authenticate: it will make sure that the requester has the authority to invoke the requested API
2. validate: the kube API server will validate the request
3. Retrieve / store in ETCD: the kube API server will retrieve or store the needed information in ETCD
4. update the user that the action is done or with a failure message
5. Scheduler continously monitor the API server and when it sees that there is a new pod object without a node assigned it will call the API server to schedule the pod in the selected node.
6. Kube API server will call the kubelet of the selected node to schedule the pod
7. the kubelet will update the kube API server about the status
8. finally the kube API server will update the information in ETCD

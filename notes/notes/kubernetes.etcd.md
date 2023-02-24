---
id: l56lmmkuhgnshwhu9gyf43d
title: Etcd
desc: ""
updated: 1677164714717
created: 1677163256625
---

# ETCD

Kubernetes stores information in a **key value store** called ETCD.

This key value store can be installed separately, but if we configured our cluster using kubeadm, then kubeadm will configure ETCD as a pod in the cluster. In a high availability scenario in which we have multiple clusters each with its own control plain, we need to configure each ETCD data store to know about the other version so that we don't have any conflicts between the control planes.

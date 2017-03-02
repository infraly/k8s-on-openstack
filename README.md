k8s-on-openstack
================

An opiniated way to deploy a Kubernetes cluster on top of an OpenStack cloud.

It is based on the following tools:

  * `kubeadm`
  * `ansible`
  * `weave-net`

Spin up a new cluster:

```console
$ ansible-playbook site.yaml
```

Destroy the cluster:

```console
$ ansible-playbook cleanup.yaml
```
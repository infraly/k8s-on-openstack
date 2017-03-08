k8s-on-openstack
================

An opiniated way to deploy a Kubernetes cluster on top of an OpenStack cloud.

It is based on the following tools:

  * `kubeadm`
  * `ansible`
  * `weave-net`

Getting started
---------------

Edit custom parameters in `host_vars/localhost.yaml`, defaults are coming from `group_vars/all.yaml`:

  * `name`: name of the Kubernetes cluster, used to derive instance names, `kubectl` configuration and security group name
  * `cloud`: name of the target OpenStack cloud, usually defined in `~/.config/openstack/clouds.yaml`
  * `image_name``: name of an existing Ubuntu 16.04 image 
  * `key_name`: name of an existing SSH keypair
  * `node_memory`: how many MB of memory should instances have
  * `node_count`: how many instances should we provision

Spin up a new cluster:

```console
$ ansible-playbook site.yaml
```

Destroy the cluster:

```console
$ ansible-playbook site.yaml -e state=absent
```

References
----------

  * https://kubernetes.io/docs/getting-started-guides/kubeadm/
  * https://www.weave.works/docs/net/latest/kube-addon/
  * https://github.com/kubernetes/dashboard#kubernetes-dashboard

k8s-on-openstack
================

An opinionated way to deploy a Kubernetes cluster on top of an OpenStack cloud.

It is based on the following tools:

  * `kubeadm`
  * `ansible`
  * `weave-net`

Getting started
---------------

The following mandatory environment variables need to be set before calling `ansible-playbook`:

  * `OS_*`: standard OpenStack environment variables such as `OS_AUTH_URL`, `OS_USERNAME`, ...
  * `KEY`: name of an existing SSH keypair

The following optional environment variables can also be set:

  * `NAME`: name of the Kubernetes cluster, used to derive instance names, `kubectl` configuration and security group name
  * `IMAGE``: name of an existing Ubuntu 16.04 image
  * `NODE_MEMORY`: how many MB of memory should instances have, defaults to 4GB
  * `NODE_COUNT`: how many instances should we provision, defaults to 3
  * `NETWORK`: name of the network to which instances should be connected
  * `FLOATING_IP_POOL`: name of the floating IP pool
  * `STATE`: set to `present` by default and must be set to `absent` to destroy the cluster

Spin up a new cluster:

```console
$ ansible-playbook site.yaml
```

Destroy the cluster:

```console
$ STATE=absent ansible-playbook site.yaml
```

CI/CD
-----

The following environment variables needs to be defined:

  * `OS_AUTH_URL`
  * `OS_PASSWORD`
  * `OS_USERNAME`

Author
------

  * François Deppierraz <francois.deppierraz@infraly.ch>

References
----------

  * https://kubernetes.io/docs/getting-started-guides/kubeadm/
  * https://www.weave.works/docs/net/latest/kube-addon/
  * https://github.com/kubernetes/dashboard#kubernetes-dashboard

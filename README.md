k8s-on-openstack
================

An opinionated way to deploy a Kubernetes cluster on top of an OpenStack cloud.

It is based on the following tools:

  * `kubeadm`
  * `ansible`

Getting started
---------------

The following mandatory environment variables need to be set before calling `ansible-playbook`:

  * `OS_*`: standard OpenStack environment variables such as `OS_AUTH_URL`, `OS_USERNAME`, ...
  * `KEY`: name of an existing SSH keypair

The following optional environment variables can also be set:

  * `NAME`: name of the Kubernetes cluster, used to derive instance names, `kubectl` configuration and security group name
  * `IMAGE`: name of an existing Ubuntu 16.04 image
  * `EXTERNAL_NETWORK`: name of the neutron external network, defaults to 'public'
  * `FLOATING_IP_POOL`: name of the floating IP pool
  * `FLOATING_IP_NETWORK_UUID`: uuid of the floating IP network (required for LBaaSv2)
  * `NODE_MEMORY`: how many MB of memory should nodes have, defaults to 4GB
  * `NODE_FLAVOR`: allows to configure the exact OpenStack flavor name or ID to use for the nodes. When set, the `NODE_MEMORY` setting is ignored.
  * `NODE_COUNT`: how many nodes should we provision, defaults to 3
  * `NODE_AUTO_IP` assign a floating IP to nodes, defaults to False
  * `NODE_DELETE_FIP`: delete floating IP when node is destroyed, defaults to True
  * `MASTER_BOOT_FROM_VOLUME`: boot the master instance on a volume for data persistence, defaults to True
  * `MASTER_TERMINATE_VOLUME`: delete the volume when master instance is destroy, defaults to True
  * `MASTER_VOLUME_SIZE`: size of the master volume
  * `MASTER_MEMORY`: how many MB of memory should master have, defaults to 4 GB
  * `MASTER_FLAVOR`: allows to configure the exact OpenStack flavor name or ID to use for the master. When set, the `MASTER_MEMORY` setting is ignored.
  * `INCLUDE_HELM`: installs helm to the cluster, defaults to False
  * `HELM_REPOS`: a list of additional helm repos to add, separated by semicolons. Example: `charts* https://github.com/helm/charts;mycharts https://github.com/dev/mycharts`
  * `HELM_INSTALL`: a list of helm charts and their parameters to install, separated by semicolons. Example: `mycharts/mychart;charts/somechart --name somechart --namespace somenamespace`
  
Spin up a new cluster:

```console
$ ansible-playbook site.yaml
```

Destroy the cluster:

```console
$ ansible-playbook destroy.yaml
```

Prerequisites
-------------

  * Ansible (tested with version 2.4 but probably also works with older ones)
  * Shade library required by Ansible OpenStack modules (`python-shade` for Debian)

CI/CD
-----

The following environment variables needs to be defined:

  * `OS_AUTH_URL`
  * `OS_PASSWORD`
  * `OS_USERNAME`
  * `OS_DOMAIN_NAME`

Authors
------

  * François Deppierraz <francois.deppierraz@infraly.ch>
  * Oli Schacher <oli.schacher@switch.ch>
  * Saverio Proto <saverio.proto@switch.ch>

References
----------

  * https://kubernetes.io/docs/getting-started-guides/kubeadm/
  * https://www.weave.works/docs/net/latest/kube-addon/
  * https://github.com/kubernetes/dashboard#kubernetes-dashboard

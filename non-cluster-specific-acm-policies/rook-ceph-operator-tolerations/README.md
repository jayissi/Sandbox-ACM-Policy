Rook Ceph Operator Tolerations
==============================

<br />

Summary
-------

Configmap `rook-ceph-operator-config` update to tolerate machine taints

<br />

Description
-----------

Dedicated nodes (i.e. `infra` and `storage`), typically have custom taints that will not be able to use OpenShift Data Foundation Persistent Volume Claims (PVCs) on the node[^1]. Toleration(s) on CSI-Plugin daemonset, `csi-cephfsplugin` and `csi-rbdplugin`, must be applied via configmap to run on all nodes where applications need to mount a Persistent Volume (PV) from Red Hat OpenShift Data Foundation (OCS) StorageClass.

[^1]: [Managing container storage interface (CSI) component placements](https://access.redhat.com/documentation/en-us/red_hat_openshift_data_foundation/4.10/html/managing_and_allocating_storage_resources/managing-container-storage-interface-component-placements_rhodf)

<br />

Verified Versions
-----------------

* Red Hat Openshift v4.10.24
* Red Hat Advanced Cluster Management v2.5.1
* Helm v3.9.4

<br />

Requirements
------------

**Red Hat OpenShift**
* Openshift version: 4.10.24 or higher

**Advanced Cluster Management**
* ACM version: 2.5.1 or higher

**Helm**
* Helm version: 3.9.4 or higher

<br />

Usage
=====

<br />

Generate Helm template

```bash
helm template .
```

<br />


Generate Helm template and submit server-side request without persisting the resource

```bash
helm template . | oc create -f - --dry-run=server
```

<br />

Create ACM policy resource

```bash
helm template . | oc create -f -
```

<br />

Variables
=========

<br />

**General Variables:**

<br />

Variable | Description | Required | Data Type | Default Value |
:------: | ----------- | :------: | :-------: | :-----------: |
`acm_policy_name` | `.metadata.name`<br>Name of this ACM policy. | yes | string |
`policy_namespace` | `.metadata.namespace`<br>Where the policy resource will be located within Openshift. | yes | string | default |
`remediation_action` | `.spec.remediation_action`<br>Specifies the remediation of your policy.<br>The parameter values are `enforce` and `inform`. | no | string | inform |
`severity` | `.spec.policy-templates[*].objectDefinition.spec.severity`<br>Specifies the severity when the policy is non-compliant.<br>The parameter values are `high`, `medium`, and `low`. | no | string | low |
`taints.<node_type>` | Specify one or more **_<node_type>_** taint for CSI plugin pods to tolerate | yes | list

<br />


Author
======

Johnny Ayissi
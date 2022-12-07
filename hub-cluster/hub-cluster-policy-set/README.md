Hub Cluster Policy Set
======================

<br />

Summary
-------

A collection of Red Hat Advance Cluster Management Policies

<br />

Description
-----------

Hub Cluster policy set is a collection of Red Hat Advance Cluster Management policies that is applicable **ONLY** to hub cluster hosted by Red Hat Advance Cluster Management (i.e. **ONLY** when cluster _local-cluster_ is _true_).

<br />

Placement Rule
--------------

```yaml
- key: local-cluster
  operator: In
  values:
  - "true"
```

Policy set placement rule states that all policies listed in var `hub_cluster.acm_policies` will be applied to every cluster in ACM labled `local-cluster="true"`

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
`acm_policy_set_name` | `.metadata.name`<br>Name of this ACM policy set. | yes | string |
`policy_set_namespace` | `.metadata.namespace`<br>Where the policy set resource will be located within Openshift. | yes | string | local-cluster-acm-policy |
`hub_cluster.acm_policies` | List of ACM policy `acm_policy_name` in the same namespace<br>as policy set applicable to clusters based on placement rule | yes | array 

<br />


Author
======

Johnny Ayissi
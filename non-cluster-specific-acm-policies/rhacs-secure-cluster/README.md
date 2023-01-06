Red Hat Advanced Cluster Security: Secured Cluster
==================================================

<br />

Summary
-------


Service to monitor and collect data to send back to Red Hat Advanced Cluster Security Central

<br />

Description
-----------

Secured Cluster installs the Collector, Sensor, and Admission Controller services[^1]. Collector collects runtime information on container security and network activity. It then sends data to Sensor, which monitors your Kubernetes cluster for policy detection and enforcement. Admission Controller monitors workloads and prevents users from creating them in RHACS when they violate security policies.

[^1]: [Secured Cluster](https://www.redhat.com/sysadmin/kubernetes-RHACS-red-hat-advanced-cluster-security)

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
helm template . -f <cluster-name>.values.yaml
```

<br />


Generate Helm template and submit server-side request without persisting the resource

```bash
helm template . -f <cluster-name>.values.yaml | oc create -f - --dry-run=server
```

<br />

Create ACM policy resource

```bash
helm template . -f <cluster-name>.values.yaml | oc create -f -
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
`node.enableTolerations` | Option to place secure cluster instance on specific node | no | boolean |
`node.selector` | Option to add node label | no | string |
`node.tolerations` | Option to add node taint for node label (if applies) | no | list |

<br />


Author
======

Johnny Ayissi
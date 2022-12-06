Openshift Proxy Certificate
===========================

<br />

Summary
-------

Proxy certificates allow users to specify one or more custom certificate authority (CA) certificates used by platform components when making egress connections.

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
`cluster_name` | Name of _<cluster_name>_ labeled in RHACM | yes | string | RHACM label<br>`name=<cluster_name>` |
`http_proxy` | A proxy URL to use for creating HTTP connections outside the cluster | no | string |
`https_proxy` | A proxy URL to use for creating HTTPS connections outside the cluster | no | string |
`no_proxy_domain` | Comma-separated list of destination domain names, domains, IP addresses or other network CIDRs to exclude proxying | no | comma-list |
`ca_cert_configmap_name` | A reference to the ConfigMap in the `openshift-config` namespace that contains additional CA certificates required for proxying HTTPS connections | yes | string |

<br />


Author
======

Johnny Ayissi

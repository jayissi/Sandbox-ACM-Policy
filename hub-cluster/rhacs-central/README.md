Red Hat Advanced Cluster Security: Central
==========================================

<br />

Summary
-------

Central service provides access to a user interface through a web UI or the RHACS portal.

<br />

Description
-----------

Central installs the Central, Scanner, and Scanner DB services[^1]. The Central service provides access to a user interface through a web UI or the RHACS portal. It also handles API interactions and provides persistent storage. Scanner analyzes images for known vulnerabilities. It uses Scanner DB as a cache for vulnerability definitions.

[^1]: [Central](https://www.redhat.com/sysadmin/kubernetes-RHACS-red-hat-advanced-cluster-security)

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
`custom_central_route_hostname` | Hostname of central's URL | no | string | central.<wildcard_domain> |
`central_storage_class_name` | StorageClass of central's PVC `stackrox-db`<br>Red Hat recommends using RBD block mode PVCs | no | string | gp2 |
`default_tls_secret` | Terminate TLS in Central and serve a custom server certificate<br>specify a secret containing the certificate and private key | no | string |
`central_root_ca_name` | Specify additional trusted Root CAs | no | string |
`node.enableTolerations` | Option to place central instance on specific node | no | boolean |
`node.selector` | Option to add node label | no | string |
`node.tolerations` | Option to add node taint for node label (if applies) | no | list |

<br />


Author
======

Johnny Ayissi

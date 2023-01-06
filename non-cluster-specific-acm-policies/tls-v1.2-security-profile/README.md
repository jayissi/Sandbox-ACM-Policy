TLSv1.2 Security Profile
========================

<br />

Summary
-------

Enforce an Openshift cluster to use TLSv1.2

<br />

Description
-----------

TLS security profiles regulate which TLS ciphers a client can use when connecting to the server[^1].

[^1]: [Openshift v4.10: TLS Security Profile](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.10/html/security_and_compliance/tls-security-profiles)


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

<br />


Author
======

Johnny Ayissi
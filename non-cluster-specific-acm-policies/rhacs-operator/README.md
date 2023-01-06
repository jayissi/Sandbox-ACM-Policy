Red Hat Advanced Cluster Security: Operator
===========================================

<br />

Summary
-------

Tool design to detect most threats and cves while providing compliance analysis and reporting.

<br />

Description
-----------

Red Hat Advanced Cluster Security for Kubernetes (RHACS) is an enterprise-ready, Kubernetes-native container security solution that protects your vital applications across build, deploy, and runtime stages of the application lifecycle[^1]. It deploys in your infrastructure and integrates with your DevOps tooling and workflows to deliver better security and compliance and to enable DevOps and InfoSec teams to operationalize security.

[^1]: [Red Hat Advanced Cluster Security for Kubernetes](https://docs.openshift.com/acs/3.72/release_notes/372-release-notes.html)

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

<br />


Author
======

Johnny Ayissi
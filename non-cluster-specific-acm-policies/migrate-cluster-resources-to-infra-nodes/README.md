Migrate Cluster Resources to Infra Nodes
========================================

<br />

Summary
-------

Designate cluster resource pod placement

<br />

Description
-----------

This template restricts the pods of Openshift's DNS, ingress controller, internal image registry, and/or monitoring stack (i.e. cluster resources) to specific node(s) based on nodeSelector and nodeTolerations set in `vaules.yaml` file. Typically during Day 2 operations, admins would migrate cluster resource pods to the **_infra_** machine-sets.

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
`migrate_openshift_dns` | Option to migrate Openshift DNS pods.<br>The parameter values are `true` and `false`. | no | boolean | true |
`migrate_ingress_controller` | Option to migrate Openshift ingress pods.<br>The parameter values are `true` and `false`. | no | boolean | true |
`migrate_image_registry` | Option to migrate Openshift internal image registry pods.<br>The parameter values are `true` and `false`. | no | boolean | true |
`migrate_openshift_monitoring` | Option to migrate Openshift monitoring stack.<br>The parameter values are `true` and `false`. | no | boolean | true |
`ingress_controller_replicas` | Define number of replica pods for ingress controller. | no | integer | 3 |
`image_registry_replicas` | Define number of replica pods for internal image registry. | no | integer | 3 |

<br />


Author
======

Johnny Ayissi
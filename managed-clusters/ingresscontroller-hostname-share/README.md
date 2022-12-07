IngressController Hostname Share
================================

<br />

Summary
-------

Allows routes to claim different paths of the same hostname across namespaces[^1].

[^1]: [InterNamespaceAllowed](https://access.redhat.com/documentation/en-us/openshift_container_platform/4.10/html/networking/configuring-ingress#nw-route-admission-policy_configuring-ingress)

<br />

Description
-----------

In the example below, both routes (_route-a_ and _route-b_) from two different namespaces will have access to the same route hostname (_redhat.apps.example.com_) but different paths once the Ingress Controller allows InterNamespace route admission policy.

<br />

**Before Change**
```bash
$ oc get route route-a -n project-a
NAME      HOST/PORT                 PATH    SERVICES    PORT    TERMINATION   WILDCARD
route-a   redhat.apps.example.com   /svca   service-a   443                   None


$ oc get route route-b -n project-b
NAME      HOST/PORT                 PATH     SERVICES    PORT   TERMINATION   WILDCARD
route-b   HostAlreadyClaimed        /svcb    service-b   443                  None
```

<br />

**Change**
```bash
$ oc patch ingresscontroller/default \
   --type=merge \
   -n openshift-ingress-operator \
   --patch '{"spec":{"routeAdmission":{"namespaceOwnership":"InterNamespaceAllowed"}}}'
```

<br />

**After Change**
```bash
$ oc get route route-a -n project-a 
NAME      HOST/PORT                 PATH    SERVICES    PORT    TERMINATION   WILDCARD
route-a   redhat.apps.example.com   /svca   service-a   443                   None


$ oc get route route-b -n project-b
NAME      HOST/PORT                 PATH    SERVICES    PORT    TERMINATION   WILDCARD
route-b   redhat.apps.example.com   /svcb   service-b   443                   None
```

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

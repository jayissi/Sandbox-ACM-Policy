Shared Secure Cluster Secrets
=============================

<br />

Summary
-------

Applying init-bundle secrets to clusters managed by Red Hat Advanced Cluster Management

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

Author
======

Johnny Ayissi

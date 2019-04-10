---
layout: default
title: "Kubernetes notifications"
---

When using Pipelines for Containers to build and deploy to Kubernetes, notifications can be configured. These notifications include:

<ul>
  <li>When build starts.</li>
  <li>When build completes.</li>
  <li>When deploy starts.</li>
  <li>When deploy completes.</li>
</ul>

Failed builds or deploys are considered completed and will notify stating the event failed.

Build events are configured in a project.

Deploy events are configured in a cluster.

Notifications can be sent/received via 3 methods:

<ul>
  <li>eMail</li>
  <li>HipChat</li>
  <li>Slack</li>
</ul>

## Build notifications

Pipelines Kubernetes build notifications are configured in a project.

Build notifications are specific to a container.

<h3>Create Build Notification</h3>

To create a build notification, you must first have a project.

<ol>
  <li>In a project, click the <b>Notifications</b> tab.</li>
  <li>On the right, select which <b>container build</b> you wish to be notified about.</li>

  <img src="images/k8s-notification-build.png" alt="Build Notifications">

  <li>Select the <b>Type</b> of notification.</li>
  <li>Select the <b>Medium</b> for notifications.</li>

  <img src="images/k8s-notification-build-types.png" alt="Build Notifications">

  <li>Select the <b>Recepient</b>.</li>
  <li>Click <b>Add Notification</b>.</li>
</ol>

## Deploy notifications

Pipelines Kubernetes deploy notifications are configured in a project.

Deploy notifications are specific to a cluster namespace.

<h3>Create Deploy Notification</h3>

To create a deploy notification, you must first have a project and a cluster.

<ol>
  <li>In a project, click the <b>Notifications</b> tab.</li>
  <li>On the bottom right, select which <b>cluster</b> you wish to be notified about deployments.</li>

  <img src="images/k8s-notification-deploy.png" alt="Build Notifications">

  <li>Select the <b>namespace</b> to set notifications.</li>
  <li>Select the <b>Type</b> of notification.</li>
  <li>Select the <b>Medium</b> for notifications.</li>

  <img src="images/k8s-notification-deploy-types.png" alt="Build Notifications">

  <li>Select the <b>Recepient</b>.</li>
  <li>Click <b>Add Notification</b>.</li>
</ol>






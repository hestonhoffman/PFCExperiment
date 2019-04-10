---
layout: default
title: "Projects"
---

A Project, in Pipelines for Containers, allows you to group one or more images for container deployments to clusters.

A projects images can be added to the project from either a software repository or a docker registry. Each image in the project can come from a different source.

If an image is added from a software repository, Pipelines can build the image. This build can be automated on commits, pull requests, and/or tags to the branch.

<img src="images/k8s-projects1.png" alt="K8S Project">

With Project pipelines you can automate the build and deploy of your images/containers to clusters.

## Create a project

Creating projects in Pipelines is easy. It is strongly recommended that you first connect your <a href="./integrate.html">Integrations</a> before creating your first project.

<h4>Step 1. Pipelines for Containers</h4>

To create a project, first ensure you are in the <b>Pipelines for Containers</b> view.

<img src="images/k8s-select-dashboard.png" alt="Select Pipelines for Containers">

You can select the Pipelines for Containers from the top left of the Pipelines web UI.


<h4>Step 2. New Project</h4>

Click the <b>New Project</b> button.

<img src="images/k8s-new-project.png" alt="New K8S Project">

Fill in the <b>Project Name</b> and the <b>Project Description</b>.

<img src="images/k8s-new-proj-details.png" alt="New K8S Project">

Click <b>Create Project</b> when you are ready.


<h4>Next Steps</h4>

For next steps, see <a href="./container.html">Adding Containers to a Project</a>.

## Create a deployment

Pipelines for Containers works directly with Kubernetes deployment specifications in YAML format.

Below is an example:

~~~
  apiVersion: extensions/v1beta1
  kind: Deployment
  metadata:
    name: k8s-mysql
  spec:
    revisionHistoryLimit: 3
    minReadySeconds: 10
    strategy:
      type: RollingUpdate
      rollingUpdate:
        maxUnavailable: 10%
        maxSurge: 10%
    replicas: 1
    template:
      metadata:
        labels:
          app: mysql
      spec:
        containers:
        - name: k8s-mysql
          image: doct15/k8s-mysql:134666
          ports:
          - containerPort: 3306
            hostPort: 3306
            protocol: TCP
            name: mysql
          volumeMounts:
          - mountPath: /etc/mysql
            name: mysql-etc
          - mountPath: /var/lib/mysql
            name: mysql-varlib
        volumes:
        - name: mysql-etc
          emptyDir: {}
        - name: mysql-varlib
          emptyDir: {}
~~~

> **Note:** Before a Kubernetes deployment spec can be created in Pipelines, the cluster and namespace where the deployment is to occur must already exist in Pipelines for Containers.


<h3>Create Deployment</h3>


<ol>
  <li>Navigate to an existing <b>project</b> in Pipelines. It is not important which one.</li>
  <li>In the top right, click the <b>Rocket</b> deploy icon.</li>

  <img src="images/k8s-deploy-icon-rocket.png" alt="Deploy Icon">

  <li>Select the <b>Cluster</b> you wish to create a deployment spec for.</li>

  <img src="images/k8s-deploy-to-cluster.png" alt="Deploy to Cluster">

  <li>Click <b>Create a new deployment</b>.</li>
  <li>Paste in your Kubernetes deployment specification <b>YAML</b>.</li>

  <img src="images/k8s-deploy-spec.png" alt="Deployment spec">

  <li>Give the deployment a <b>Deployment Description (required)</b>.</li>
  <li>Click <b>Deploy</b> to finish.</li>
</ol>

This will create the deployment specification and initiate an initial deploy to the cluster as defined in the specification.

This deployment specification is now available to add to a project pipeline.


<h3>Deploy Success</h3>


A deployment specification that does not have a <code>minReadySeconds</code> field specified (The field that tells Kubernetes how many seconds a new pod should be up for without crashing before being marked as available), will be judged as a success if the up-to-date number of pods reaches the desired number of pods. 

A deployment specification that has the <code>minReadySeconds</code> field specified will be deemed a success once the up-to-date and available number of pods reaches the desired number of pods. 

<h3>Next Steps</h3>

<a href="./container-pipeline.html">Set Auto-Deploy in a Pipeline</a>

## Create a service

<br/>

Pipelines works directly with Kubernetes service specifications in YAML format.

Below is an example:

~~~
apiVersion: v1
kind: Service
metadata:
  name: k8s-mysql
spec:
  ports:
    - port: 3306
      protocol: TCP
      targetPort: 3306
  selector:
    deployment: k8s-mysql
    run: k8s-mysql
  type: LoadBalancer
~~~

> **Note:** Before a Kubernetes service spec can be created, in Pipelines, the cluster and namespace where the service is to live must already exist in Pipelines.



<h3>Create Service</h3>


<ol>
  <li>Navigate to an existing <b>project</b> in Pipelines. It is not important which one.</li>
  <li>In the top right, click the <b>Service</b> icon.</li>

  <img src="images/k8s-service-icon-services.png" alt="Deploy Icon">

  <li>Select the <b>Cluster</b> you wish to create a service for.</li>
  <li>Click <b>Create a new service</b> button.</li>
  <li>Paste in your Kubernetes service specification <b>YAML</b>.</li>

  <img src="images/k8s-service-spec.png" alt="Deployment spec">

  <li>Click <b>Create Service</b> to finish.</li>
</ol>

This will create the service specification and configure the cluster with the service.

Services may take a couple minutes to provision in the cluster.









---
layout: default
title: "Cluster namespaces"
--- 

Namespaces allow you to partition your cluster into separate logical areas.

With Pipelines role based access control, permission to a namespace can be locked down to specific users.

## Create a Namespace

To create a namespace in your cluster:

<ol>
  <li>Select <b>Clusters</b> from the top menu in the Pipelines for Containers web UI.</li>
  <li>From the list of clusters being managed by Pipelines, select the one you wish to add a namespace to.</li>
  <li>Click the <b>Namespace Settings</b> gear to the right.</li>

  <img src="images/europak8s-namespace-settings.png" alt="Namespace Settings">

  <p>You will see the <b>Add/Remove Namespaces</b> control room.</p>

  <img src="images/europak8s-namespace-add-remove.png" alt="Namespace Settings add remove">
  
  <li>Click the <b>Create Namespace</b> button.</li>
  <li>Enter a <b>Name</b> for the namespace.</li>
  <li>Click <b>Create</b> to create the namespace.</li>
</ol>

You have created a new namespace in your cluster.

## Remove a Namespace

Follow the above instructions to navigate to the <b>Namespace Settings</b>.

Click the <b>trash can icon</b> to delete a namespace.

<img src="images/europak8s-namespace-trash.png" alt="Namespace Settings add remove">

> **Note:** Some existing namespaces are critical to the Kubernetes system and should not be removed. Removing one could render your cluster unusable.

## Create namespace secrets

<h3>Create Secrets</h3>

You can manage your cluster namespace secrets from a project or from a cluster details page. The experience is the same.

<ol>
  <li>Click the <b>Secrets</b> tab.</li>

  <img src="images/europak8s-secrets-icon.png" alt="Secrets icon">

  <li>Select (click) the <b>Cluster</b> you wish to manage secrets.</li>

  <p>You will be shown all of the existing namespace secrets in the chosen cluster.</p>

  <li>Click <b>+ Add New Secret</b>.</li>
  <li>Select the <b>Namespace</b> you wish to manage secrets.</li>
  <li>Enter a <b>Secret Name</b> for your secrets.</li>
  <li>Now enter the secrets as <b>key=value</b>. You can enter multiples, one per line. Below is an example.</li>

  <img src="images/europak8s-create-new-secrets-europa.png" alt="Create new Secrets">

  <li>When you are ready, click <b>Create Secret</b>.</li>
</ol>

You have created cluster namespace secrets. These secrets are available during deployment in the <b>env</b> container section of the Kubernetes deployment specification.

~~~
env:
  - name: EUROPA_DB_ENDPOINT
    valueFrom:
      secretKeyRef:
        key: EUROPA_DB_ENDPOINT
        name: europa
~~~


Here is an example deployment specification that leverages the above example secrets.

~~~
apiVersion: extensions/v1beta1
kind: Deployment
metadata:
  name: europa
  namespace: europa
spec:
  replicas: 1
  strategy:
    rollingUpdate:
      maxSurge: 1
      maxUnavailable: 1
    type: RollingUpdate
  template:
    metadata:
      labels:
        deployment: europa
        app: europa
    spec:
      containers:
        - name: europa
          image: distelli/europa:latest
          ports:
          - containerPort: 80
            hostPort: 80
            protocol: TCP
            name: http
          - containerPort: 443
            hostPort: 443
            protocol: TCP
            name: https
          env:
            - name: EUROPA_DB_ENDPOINT
              valueFrom:
                secretKeyRef:
                  key: EUROPA_DB_ENDPOINT
                  name: europa
            - name: EUROPA_DB_USER
              valueFrom:
                secretKeyRef:
                  key: EUROPA_DB_USER
                  name: europa
            - name: EUROPA_DB_PASS
              valueFrom:
                secretKeyRef:
                  key: EUROPA_DB_PASS
                  name: europa
          volumeMounts:
          - mountPath: /europa/repo
            name: europa-disk
            subPath: europa/repo
        - name: mysql
          image: mysql/mysql-server:5.7
          ports:
          - containerPort: 3306
            hostPort: 3306
            protocol: TCP
            name: mysql
          env:
            - name: MYSQL_ROOT_PASSWORD
              valueFrom:
                secretKeyRef:
                  key: MYSQL_ROOT_PASSWORD
                  name: europa
            - name: MYSQL_DATABASE
              valueFrom:
                secretKeyRef:
                  key: MYSQL_DATABASE
                  name: europa
            - name: MYSQL_USER
              valueFrom:
                secretKeyRef:
                  key: MYSQL_USER
                  name: europa
            - name: MYSQL_PASSWORD
              valueFrom:
                secretKeyRef:
                  key: MYSQL_PASSWORD
                  name: europa
            - name: MYSQL_ROOT_HOST
              valueFrom:
                secretKeyRef:
                  key: MYSQL_ROOT_HOST
                  name: europa
          volumeMounts:
          - mountPath: /var/lib/mysql
            name: europa-disk
            subPath: var/lib/mysql
      volumes:
      - name: europa-disk
        gcePersistentDisk:
          pdName: europa
      dnsPolicy: ClusterFirst
      restartPolicy: Always
~~~

## Edit Secrets

Follow the procedures above to navigate to the cluster secrets.

Click the <b>edit icon</b> to the right of a secret name to edit it.

<img src="images/europak8s-edit-secrets.png" alt="Edit Secrets">


## Delete Secrets

Follow the procedures above to navigate to the cluster secrets.

Click the <b>trash can icon</b> to the right of a secret name to delete it.

<img src="images/europak8s-delete-secrets.png" alt="Delete Secrets">

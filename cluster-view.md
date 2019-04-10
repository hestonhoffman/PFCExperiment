---
layout: default
title: "Viewing clusters"
--- 

Pipelines provides in-depth information on your cluster for you to quickly see and filter.

A cluster must be added to Pipelines to be viewed in Pipelines. For more information on adding a cluster see [Adding clusters](./cluster-add.html).

## View a cluster

<img src="images/cview-clustericon.png" alt="Cluster Details">

To view a cluster's details:

<ol>
  <li>Ensure you are in the <b>Pipelines for Containers web UI</b>.</li>
  <li>Click <b>Clusters</b> at the top.</li>
  <li>Click the <b>Cluster</b> you wish to see details for.</li>
</ol>

The cluster details page will open.

<img src="images/cview-header1.png" alt="Cluster Details">

At the top of the Cluster details you will see the cluster core information.

The namespace selector will allow the balance of the details to be filtered by namespace.

<h3>Cluster Notifications</h3>
<img src="images/cview-notificationsicon.png" alt="Cluster Details">

Click the <b>Notifications</b> link to see deploy notifications.

<img src="images/cview-notifications1.png" alt="Deploy Notifications Details">

<h3>Cluster Credentials</h3>
<img src="images/cview-credentialsicon.png" alt="Cluster Details">

Click the <b>Credentials</b> link to see the cluster credentials.

<img src="images/cview-credentials1.png" alt="Cluster Certificates">

## View cluster deployments

<h3>View a Cluster's Deployments</h3>

To view a cluster's deployments:

<ol>
  <li>Ensure you are on the <b>Pipelines for Containers web UI</b>.</li>
  <li>Click <b>Clusters</b> at the top.</li>
  <li>Click the <b>Cluster</b> you wish to see details for.</li>
  <li>Filter the details by <b>Namespace</b>.</li>
</ol>

Here you can see the cluster kubernetes deployment objects.


<img src="images/cview-deployments1.png" alt="Cluster Deployments">

<h4>View Details</h4>

This option will show you the deployment information directly from the cluster.

~~~
{
  metadata:
  Object: {
    annotations:
    Object: {
      deployment.kubernetes.io/revision:1
    }
    creationTimestamp:2016-12-28T01:02:18Z
    generation:2
    labels:
    Object: {
      app:mysql
      deployment:k8s-mysql
      distelli:d461
    }
    name:k8s-mysql
    namespace:default
    resourceVersion:388
    selfLink:/apis/extensions/v1beta1/namespaces/default/deployments/k8s-mysql
    uid:478a3886-cc99-11e6-a240-42010a8a0068
  }
  spec:
  Object: {
    minReadySeconds:10
    replicas:1
    revisionHistoryLimit:3
    selector:
    Object: {
      matchLabels:
      Object: {
        app:mysql
        deployment:k8s-mysql
        distelli:d461
      }
    }
    strategy:
    Object: {
      rollingUpdate:
      Object: {
        maxSurge:10%
        maxUnavailable:10%
      }
      type:RollingUpdate
    }
    template:
    Object: {
      metadata:
      Object: {
        annotations:
        Object: {
          kubernetes.io/change-cause:bm1
        }
        labels:
        Object: {
          app:mysql
          deployment:k8s-mysql
          distelli:d461
        }
      }
      spec:
      Object: {
        containers:
        Array: [
          Object: {
            image:doct15/k8s-mysql:134666
            imagePullPolicy:IfNotPresent
            name:k8s-mysql
            ports:
            Array: [
              Object: {
                containerPort:3306
                hostPort:3306
                name:mysql
                protocol:TCP
              }
            ]
            resources:Object: {}
            terminationMessagePath:/dev/termination-log
            volumeMounts:
            Array: [
              Object: {
                mountPath:/etc/mysql
                name:mysql-etc
              },
              Object: {
                mountPath:/var/lib/mysql
                name:mysql-varlib
              }
            ]
          }
        ]
        dnsPolicy:ClusterFirst
        restartPolicy:Always
        securityContext:Object: {}
        terminationGracePeriodSeconds:30
        volumes:
        Array: [
          Object: {
            emptyDir:Object: {}
            name:mysql-etc
          },
          Object: {
            emptyDir:Object: {}
            name:mysql-varlib
          }
        ]
      }
    }
  }
  status:
  Object: {
    availableReplicas:1
    observedGeneration:2
    replicas:1
    updatedReplicas:1
  }
}
~~~

<h4>View Pods</h4>

Selecting this will filter the pods (replica sets) on the left to just the ones associated with this deployment.

<img src="images/cview-podfilter1.png" alt="Filter Pods">

<h4>Delete Deployment</h4>

Selecting this will allow you to delete the deployment. You will be prompted to confirm the deletion.

> **Note:** Currently when doing a delete deployment, Pipelines does not cascade the deletion thus the replica sets and pods will remain.

## View a cluster's pods

To view a cluster's deployments:

<ol>
  <li>Ensure you are on the <b>Pipelines for Containers web UI</b>.</li>
  <li>Click <b>Clusters</b> at the top.</li>
  <li>Click the <b>Cluster</b> you wish to see details for.</li>
  <li>Filter the details by <b>Namespace</b>.</li>
</ol>

Here you can see the cluster pods and replication information.

<img src="images/cview-pods2.png" alt="Cluster Pods">

<h4>View Details</h4>

This option will show you the replica set information directly from the cluster.

~~~
{
  metadata:
  Object: {
    annotations:
    Object: {
      kubernetes.io/change-cause:bm1
      kubernetes.io/created-by:{"kind":"SerializedReference","apiVersion":"v1","reference":{"kind":"ReplicaSet","namespace":"default","name":"k8s-mysql-3877443125","uid":"478b22a9-cc99-11e6-a240-42010a8a0068","apiVersion":"extensions","resourceVersion":"298"}}
      kubernetes.io/limit-ranger:LimitRanger plugin set: cpu request for container k8s-mysql
    }
    creationTimestamp:2016-12-28T01:02:18Z
    generateName:k8s-mysql-3877443125-
    labels:
    Object: {
      app:mysql
      deployment:k8s-mysql
      distelli:d461
      pod-template-hash:3877443125
    }
    name:k8s-mysql-3877443125-1pzel
    namespace:default
    ownerReferences:
    Array: [
      Object: {
        apiVersion:extensions/v1beta1
        controller:true
        kind:ReplicaSet
        name:k8s-mysql-3877443125
        uid:478b22a9-cc99-11e6-a240-42010a8a0068
      }
    ]
    resourceVersion:337
    selfLink:/api/v1/namespaces/default/pods/k8s-mysql-3877443125-1pzel
    uid:478cd119-cc99-11e6-a240-42010a8a0068
  }
  spec:
  Object: {
    containers:
    Array: [
      Object: {
        image:doct15/k8s-mysql:134666
        imagePullPolicy:IfNotPresent
        name:k8s-mysql
        ports:
        Array: [
          Object: {
            containerPort:3306
            hostPort:3306
            name:mysql
            protocol:TCP
          }
        ]
        resources:
        Object: {
          requests:
          Object: {
            cpu:100m
          }
        }
        terminationMessagePath:/dev/termination-log
        volumeMounts:
        Array: [
          Object: {
            mountPath:/etc/mysql
            name:mysql-etc
          },
          Object: {
            mountPath:/var/lib/mysql
            name:mysql-varlib
          },
          Object: {
            mountPath:/var/run/secrets/kubernetes.io/serviceaccount
            name:default-token-1gip9
            readOnly:true
          }
        ]
      }
    ]
    dnsPolicy:ClusterFirst
    nodeName:gke-docs-default-pool-38c20d7e-2l34
    restartPolicy:Always
    securityContext:Object: {}
    serviceAccount:default
    serviceAccountName:default
    terminationGracePeriodSeconds:30
    volumes:
    Array: [
      Object: {
        emptyDir:Object: {}
        name:mysql-etc
      },
      Object: {
        emptyDir:Object: {}
        name:mysql-varlib
      },
      Object: {
        name:default-token-1gip9
        secret:
        Object: {
          secretName:default-token-1gip9
        }
      }
    ]
  }
  status:
  Object: {
    conditions:
      Array: [
        Object: {
          lastTransitionTime:2016-12-28T01:02:18Z
          status:True
          type:Initialized
        },
        Object: {
          lastTransitionTime:2016-12-28T01:02:36Z
          status:True
          type:Ready
        },
        Object: {
          lastTransitionTime:2016-12-28T01:02:18Z
          status:True
          type:PodScheduled
        }
      ]
      containerStatuses:
      Array: [
        Object: {
          containerID:docker://6ede89a828c1752b3e79040542d7ea62fc4411f175e8185893a1b15b1bef6d2c
          image:doct15/k8s-mysql:134666
          imageID:docker://sha256:f055d50837008b785236988a22c7476866662d5e7a0453b043fea1b39d89e7cc
          lastState:Object: {}
          name:k8s-mysql
          ready:true
          restartCount:0
          state:
          Object: {
            running:
            Object: {
              startedAt:2016-12-28T01:02:36Z
            }
          }
        }
      ]
      hostIP:10.138.0.5
      phase:Running
      podIP:10.56.1.4
      startTime:2016-12-28T01:02:18Z
    }
  }
~~~


<h4>View Logs</h4>

Selecting this will allow you to see the live logging in the Pod.


<img src="images/cview-pod-logs.png" alt="Pod Logs">

## View cluster services

To view a cluster's deployments:

<ol>
  <li>Ensure you are on the <b>Pipelines for Containers web UI</b>.</li>
  <li>Click <b>Clusters</b> at the top.</li>
  <li>Click the <b>Cluster</b> you wish to see details for.</li>
  <li>Filter the details by <b>Namespace</b>.</li>
</ol>

Here you can see the cluster kubernetes services objects.


<img src="images/cview-services1.png" alt="Cluster services">

<h4>View Details</h4>

This option will show you the service information directly from the cluster.

~~~
{
  metadata:
  Object: {
    creationTimestamp:2016-12-28T01:05:18Z
    name:k8s-mysql
    namespace:default
    resourceVersion:736
    selfLink:/api/v1/namespaces/default/services/k8s-mysql
    uid:b2fddf0f-cc99-11e6-a240-42010a8a0068
  }
  spec:
  Object: {
    clusterIP:10.59.255.215
    ports:
    Array: [
      Object: {
        nodePort:31872
        port:3306
        protocol:TCP
        targetPort:3306
      }
    ]
    selector:
    Object: {
      deployment:k8s-mysql
      run:k8s-mysql
    }
    sessionAffinity:None
    type:LoadBalancer
  }
  status:
  Object: {
    loadBalancer:
    Object: {
      ingress:
      Array: [
        Object: {
          ip:104.198.1.184
        }
      ]
    }
  }
}
~~~


<h4>View Pods</h4>

Selecting this will filter the pods (replica sets) on the left to just the ones associated with this service.

<img src="images/cview-podfilter1.png" alt="Filter Pods">


<h4>Delete Service</h4>

Selecting this will allow you to delete the service. You will be prompted to confirm the deletion.












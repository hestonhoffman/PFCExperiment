---
layout: default
title: "Adding clusters"
--- 

With Pipelines, you can create, manage, and deploy to Docker clusters.

There are numerous types of Docker clustering platforms. These include:

<ul>
  <li>Docker Swarm</li>
  <li>Kubernetes</li>
  <li>Mesos</li>
  <li>and more...</li>
</ul>

A cluster is a grouping of server instances for deploying running Docker containers. The cluster can be treated as a single entity that dynamically runs Docker containers on appropriate resources. Clusters can provide auto-scaling of services.

## Kubernetes

Kubernetes (k8s) is an open source container cluster manager originally designed by Google. K8s works with Docker containers and coordinates a cluster of hosts running Docker. K8s provides a platform for deploying, scaling, and operations of containers across clusters of hosts.

Kubernetes is Greek for Helmsman or Pilot.

Pipelines for Containers offers advanced features for k8s cluster management, including:

<ul>
  <li>Learning of existing clusters dynamically and manually.</li>
  <li>Automated builds and deploy (CI/CD).</li>
  <li>Creating new clusters.</li>
  <li>Monitoring the cluster.</li>
  <li>Deploying containers to the cluster.</li>
  <li>Creating services.</li>
  <li>Inspecting logs.</li>
  <li>and much more...</li>
</ul>

K8s uses a command line tool called kubectl. It is available <a href="http://kubernetes.io/docs/user-guide/prereqs/" target="_blank">here</a>.

The k8s CLI requires a <a href="http://kubernetes.io/docs/user-guide/kubeconfig-file/" target="_blank">kubeconfig</a> file with information on how to connect to a cluster. This file can be downloaded from Pipelines.

## Sync clusters

The Sync Clusters feature is specifically for synchronizing clusters in Google Cloud with Pipelines.

You can synchronize with all Google Cloud Projects or only specific projects.

To synchronized your clusters with your Google Cloud Project:

1. From the Pipelines for Containers web UI, click the <b>Clusters</b> link at the top.
1. Click the <b>Sync Clusters</b> link.

> **Note:** If you have not configured your Google Cloud integrations within Pipelines, you will not have a <i>Sync Clusters</i> button, but instead a <b>Connect GCE</b>. Before continuing, click <b>Connect GCE</b> and integrate Pipelines with your GCE.

Select 1 or more projects and click <b>Update Selected Projects</b><br><b>OR</b><br>Click <b>Update All Projects</b>.
  
  <img src="images/k8s-sync-clusters.png" alt="Sync Clusters">

Pipelines will update the clusters in the GCE project(s) you have chosen. This includes learning of new ones and the removal of any deleted clusters.

## Add GKE cluster

Adding a Google Container Engine (GKE) Cluster will create a new cluster in Google Cloud that Pipelines will manage

<h3>1 - Google Credentials</h3>
<img src="images/newgcecluster-1.png" alt="New GKE Cluster Step 1">
Adding a cluster to Google Cloud will require your add your Google credentials. The credentials must have GKE IAM, Cloud Resource Manager, Compute Engine, and Container Engine API's.

<h3>2 - Select Project</h3>
<img src="images/newgcecluster-2.png" alt="New GKE Cluster Step 2">
Select which project in GKE you wish to create the kubernetes cluster. This project must have API access.

<h3>3 - Name your Cluster</h3>
<img src="images/newgcecluster-3.png" alt="New GKE Cluster Step 3">
Give the cluster a name. Names must start with a lowercase letter followed by up to 29 lowercase letters (max length is 30), numbers, or hyphens, and cannot end with a hyphen.

<h3>4 - Select Zone</h3>
<img src="images/newgcecluster-4.png" alt="New GKE Cluster Step 4">
Select the GKE zone that this cluster will be created in.

<h3>5 - Select Machine Type</h3>
<img src="images/newgcecluster-5.png" alt="New GKE Cluster Step 5">
Typically a cluster should start with at least 3 machines of the appropriate size. Select the machine type.

<h3>6 - Enter the number of nodes in your cluster</h3>
<img src="images/newgcecluster-6.png" alt="New GKE Cluster Step 6">

<h3>7 - The IP addresses of the container pods in this cluster</h3>
<img src="images/newgcecluster-7.png" alt="New GKE Cluster Step 7">
Specify a /14 block in the block 10.0.0.0/8.

<h3>8 - Enter Disk Size in GB</h3>
<img src="images/newgcecluster-8.png" alt="New GKE Cluster Step 8">
Allowable Range: 10GB - 65536GB.

<h3>9 - Configure Tags</h3>
<img src="images/newgcecluster-9.png" alt="New GKE Cluster Step 9">
For more info on GKE tags please see <a href="https://cloud.google.com/compute/docs/label-or-tag-resources" target="_blank">Label or Tag Resources</a>.

<h3>10 - Access Scopes</h3>
<img src="images/newgcecluster-10.png" alt="New GKE Cluster Step 10">
Select the <b>Access Scopes</b> as necessary.

<h3>11 - Please enter the credentials that will be used to access the cluster master endpoint</h3>
<img src="images/newgcecluster-11.png" alt="New GKE Cluster Step 11">
This will configure basic authentication credentials for access to the cluster. Pipelines does not use basic authentication to access the cluster.

<h3>12 - Launch Cluster!</h3>
<img src="images/newgcecluster-12.png" alt="New GKE Cluster Step 12">
When you are ready, click <b>Launch</b> to launch the cluster.

## Add AWS cluster

Adding an AWS Cluster will create a new cluster in AWS that Pipelines will manage

When adding a new cluster, to AWS, the selection of VPC, Subnets, and Security Groups is important in that the resulting Cluster management IP Address must be reachable by Pipelines on port 443.

<h3>1 - EC2 Credentials</h3>
<img src="images/newawscluster-1.png" alt="New AWS Cluster Step 1">
Adding a cluster to AWS will require your add your AWS credentials. The credentials must have appropriate permissions to launch EC2 instances.

<h3>2 - Select Region</h3>
<img src="images/newawscluster-2.png" alt="New AWS Cluster Step 2">
Select the AWS region.

<h3>3 - Name your Cluster</h3>
<img src="images/newawscluster-3.png" alt="New AWS Cluster Step 3">
Give the cluster a name. Names must start with a lowercase letter followed by up to 29 lowercase letters (max length is 30), numbers, or hyphens, and cannot end with a hyphen.

<h3>4 - Select Instance Type</h3>
<img src="images/newawscluster-4.png" alt="New AWS Cluster Step 4">
Typically a cluster should start with at least 3 instances of the appropriate size. Select the instance type and number of nodes.

<h3>5 - Configure Virtual Private Cloud</h3>
<img src="images/newawscluster-5.png" alt="New AWS Cluster Step 5">
Select a VPC that will have a subnet for the master subnet that includes an Internet gateway. The VPC should also have a subnet for the minion subnet that includes a NAT.

<h3>6 - Configure Master Subnet</h3>
<img src="images/newawscluster-6.png" alt="New AWS Cluster Step 6">
The master node should reside in a subnet with an Internet gateway.

<h3>7 - Configure Minion Subnet</h3>
<img src="images/newawscluster-7.png" alt="New AWS Cluster Step 7">
The minion nodes should reside in a subnet with a NAT (Network Address Translation) device.

<h3>8 - Configure Subnet IP Ranges</h3>
<img src="images/newawscluster-8.png" alt="New AWS Cluster Step 8">
Note, this IP block must be unused and available across all clusters.

<h3>9 - Configure Master Endpoint</h3>
<img src="images/newawscluster-9.png" alt="New AWS Cluster Step 9">
The Cluster master endpoint comes from an existing AWS Elastic IP.

<h3>10 - Configure Key Pairs</h3>
<img src="images/newawscluster-10.png" alt="New AWS Cluster Step 10">
The SSH key pairs will be used for access to the ec2 instances.
Pipelines does not use key pairs to access the cluster. Pipelines uses certificates to access the cluster.

<h3>11 - Configure IAM Role</h3>
<img src="images/newawscluster-11.png" alt="New AWS Cluster Step 11">
Select the IAM role for the cluster.

<h3>12 - Configure Security Groups</h3>
<img src="images/newawscluster-12.png" alt="New AWS Cluster Step 12">
Select the security group(s) for the cluster.

<h3>13 - Configure Root Partition Size (GB)</h3>
<img src="images/newawscluster-13.png" alt="New AWS Cluster Step 13">

<h3>14 - Configure EBS Volume</h3>
<img src="images/newawscluster-14.png" alt="New AWS Cluster Step 14">

<h3>15 - Configure Tags</h3>
<img src="images/newawscluster-15.png" alt="New AWS Cluster Step 15">
For more information on AWS tags, please see <a href="http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/Using_Tags.html target="_blank">AWS Using Tags</a>.

<h3>16 - Launch AWS Kubernetes Cluster!</h3>
<img src="images/newawscluster-16.png" alt="New AWS Cluster Step 16">
When you are ready, click <b>Launch Cluster</b> to launch the cluster.

## Using multiple EC2 credentials 

This feature allows the addition of multiple AWS EC2 credentials from which to launch EC2 instances. This includes launching instances for a Kubernetes cluster in AWS.

<h3>Setup Multiple EC2 credentials</h3>

To navigate to the EC2 credentials:

<ol>
    <li>Ensure you are on the <b>VM Dashboard</b>.</li>
    <li>Click the <b>Gear</b> icon at the top right of the Pipelines web UI.</li>
    <li>Click the <b>Integrations</b> link on the left.</li>
    <li>Click the <b>Amazon Web Services</b> icon.</li>
    <li>Select the <b>AWS EC2</b> tab.</li>
</ol>


You can add multiple keys by clicking the <b>Add Key</b> link.

<img src="images/m-ec2-add-keys.png" alt="ec2 add keys">

<h3>RBAC Permissions for EC2 Credentials</h3>

After adding one or more AWS EC2 credentials, a permission group can be configured to control which users have access to which credentials.

To create group permissions for access to AWS EC2 credentials:

<ol>
    <li>Ensure you are on the <b>VM Dashboard</b>.</li>
    <li>Click the <b>Gear</b> icon at the top right of the Pipelines web UI.</li>
    <li>Click the <b>Groups</b> link on the left.</li>
    <li>Either <b>Create New Group</b> or edit an existing group.</li>
    <li>Scroll to the bottom of the group permissions to find the <b>Provisioning</b> section.</li>
</ol>

From here the group permission specifies what EC2 credentials users of this group have and do not have access to.

<img src="images/m-ec2-group-permissions.png" alt="ec2 key permissions">

For more information on users and group permissions see:

* [Users](./users.html)
* [Groups](./group.html)

<h3>Using Multiple EC2 Credentials</h3>

Now, when launching EC2 instances (or EC2 clusters) a user will be prompted which credentials to use, based on the available credentials to that user.

<img src="images/m-ec2-launch.png" alt="ec2 launch">

## Add an existing cluster

Adding an existing Cluster to Pipelines will allow you to automate deployments to the cluster, and manage the cluster in Pipelines.

When adding an existing cluster to Pipelines, it is critical that the Cluster management IP Address must be reachable by Pipelines on port 443.

Connecting to a cluster will typically require, at a minimum (except GKE):

<ul>
  <li>Client certificate</li>
  <li>Client key</li>
  <li>Cluster certificate</li>
</ul>

Pipelines uses certificates for authentication. Pipelines does not use basic authentication.


<h3>Obtaining your Cluster Certificates</h3>

You can obtain your cluster certificates from a kubectrl <code>~/.kube/config</code> configuration file.

A single cluster configuration may look like this:

~~~
\-\-\-
apiVersion: "v1"
clusters:
- name: "kubernetes"
  cluster:
    certificate-authority-data: "ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEF" 
    server: "https://104.198.1.40"
contexts:
- name: "admin@kubernetes"
  context:
    cluster: "kubernetes"
    user: "admin"
current-context: "admin@kubernetes"
kind: "Config"
preferences: {}
users:
- name: "admin"
  user:
    client-certificate-data: "ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJ"
    client-key-data: "ABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZABCDEFGHIJKLMNOPQRSTUVWXYZ" 
~~~

The fields are as follows:

<table>
<tr><th>~/.kube/config field</th><th>Pipelines field</th></tr>
<tr><td>certificate-authority-data</td><td>cluster certificate</td></tr>
<tr><td>client-certificate-data</td><td>client certificate</td></tr>
<tr><td>client-key-data</td><td>client key</td></tr>
<tr><td>server</td><td>Master Endpoint IP</td></tr>
</table>

If you need to create a new certificate for Pipelines to use on your cluster, please see <a href="http://kubernetes.io/docs/user-guide/kubectl/kubectl_config_set-credentials/" target="_blank">kubectl config set-credentials</a>.

<h3>Connecting your Cluster</h3>

Depending on which cloud provider is hosting your existing clusters, Pipelines will need differing information to connect to your cluster.

<img src="images/k8s-existing-cluster.png" alt="Existing Cluster">

<h3>Connecting Google Cloud (GKE)</h3>

Please see the Sync Clusters section above.

<h3>Connecting Amazon Web Services (AWS)</h3>

If you have not already configured your AWS credentials in the [integrations](./integrate.html) page, you will be prompted to add them during the add existing cluster workflow.

<img src="images/k8s-add-new-credentials.png" alt="Add AWS credentials">

You will need to provide the following information:

<ul>
  <li><b>Enter your cluster name</b> - This name will appear in Pipelines.</li>
  <li><b>Select your cluster region</b> - The AWS region that the cluster exists in.</li>
  <li><b>Enter you Master Node Instance ID</b> - The AWS EC2 Instance ID for the cluster master node.</li>
  <li><b>Enter your Master Endpoint IP</b> - The master IPv4 endpoint address for the cluster.</li>
  <li><b>Enter your client certificate</b> - The cluster client certificate.</li>
  <li><b>Enter your client key</b> - The cluster client key.</li>
  <li><b>Enter your cluster certificate</b> - The cluster certificate.</li>
</ul>

<h3>Connecting Microsoft Azure</h3>

To connect to a Kubernetes cluster in Microsoft Azure you will need to provide the following information:

<ul>
  <li><b>Enter your cluster name</b> - This name will appear in Pipelines.</li>
  <li><b>Enter your cluster region</b> - The Azure region that the cluster exists in.</li>
  <li><b>Enter your Master Endpoint IP</b> - The master IPv4 endpoint address for the cluster.</li>
  <li><b>Enter your client certificate</b> - The cluster client certificate.</li>
  <li><b>Enter your client key</b> - The cluster client key.</li>
  <li><b>Enter your cluster certificate</b> - The cluster certificate.</li>
</ul>

<h3>Bare Metal</h3>

To connect to a Kubernetes cluster on bare metal you will need to provide the following information:

<ul>
  <li><b>Enter your cluster name</b> - This name will appear in Pipelines.</li>
  <li><b>Enter your cluster region</b> - The region that the cluster exists in.</li>
  <li><b>Enter your Master Endpoint IP</b> - The master IPv4 endpoint address for the cluster.</li>
  <li><b>Enter your client certificate</b> - The cluster client certificate.</li>
  <li><b>Enter your client key</b> - The cluster client key.</li>
  <li><b>Enter your cluster certificate</b> - The cluster certificate.</li>
</ul>

<h3>Other</h3>

To connect to a Kubernetes cluster you will need to provide the following information:

<ul>
  <li><b>Enter your cluster name</b> - This name will appear in Pipelines.</li>
  <li><b>Enter your cluster region</b> - The region that the cluster exists in.</li>
  <li><b>Enter your Master Endpoint IP</b> - The master IPv4 endpoint address for the cluster.</li>
  <li><b>Enter your client certificate</b> - The cluster client certificate.</li>
  <li><b>Enter your client key</b> - The cluster client key.</li>
  <li><b>Enter your cluster certificate</b> - The cluster certificate.</li>
</ul>


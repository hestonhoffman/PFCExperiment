---
layout: default
title: "Container pipelines"
--- 

Kubernetes pipelines provide the mechanisms to auto-build docker images and auto-deploy docker containers to Kubernetes.

<img src="images/k8s-pipeline-example.png" alt="K8S Pipeline">


After adding containers to a project, you can create a pipeline for one or more containers. In the pipeline you can specify auto-build options (aka CI Continuous Integration) and auto-deploy (CD Continuous Deployment).

Multiple pipelines can be created in a Pipelines project.

The same container can exist in multiple pipelines.

Containers in pipelines are branch specific.

Automated deploys can occur across multiple clusters and/or namespaces.

## Create a project pipeline

<ol>
  <li>Ensure you are looking at the project you want to create the pipeline in.</li>
  <li>Navigate to the <b>Pipeline</b> tab.</li>

  <img src="images/k8s-pipelines-tab.png" alt="Pipelines tab">

  <li>Click the <b>+ Create Pipeline</b> link.</li>

  <img src="images/k8s-create-pipeline.png" alt="Create Pipeline">

  <li>Enter a <b>Pipeline Name</b>.</li>

  <img src="images/k8s-name-pipeline.png" alt="Name a Pipeline">

  <li>Click <b>Create Pipeline</b> button.</li>

</ol>

You have created a pipeline for automating the builds and deploys of your containers.

Realize you can add more than one pipeline to your project.

## Add a container to a pipeline

> **Note:** Before a container can be added to a pipeline, it must first be added to the project.

<h3><a name="add-software-repository-container-to-a-pipeline"></a>Add Software Repository Container to a Pipeline</h3>

<ol>
  <li>While viewing a pipeline, click the <b>+ Add Containers</b> link.</li>

  <img src="images/k8s-add-container1.png" alt="Add Container">

  <li>Click in the field <b>Select Container</b> to select the container from the list of available containers.</li>

  <img src="images/k8s-select-container1.png" alt="Add Container">

  <li>Click in the field <b>Select Branch</b> to select the branch from the list of available branches. <b>-OR-</b> You can set a regex that will match branch(es), by clicking in the field <b>Enter Regex</b> and entering a branch matching regex.</li>

  <img src="images/k8s-select-branch1.png" alt="Select Branch">
  
  <b>-OR-</b>

  <img src="images/k8s-select-branch2.png" alt="Select Branch">

  <li>When you are ready, click the <b>Save Source</b> button.</li>
</ol>


<h3><a name="add-docker-registry-container-to-a-pipeline"></a>Add Docker Registry Container to a Pipeline</h3>

<ol>
  <li>While viewing a pipeline, click the <b>+ Add Containers</b> link.</li>

  <img src="images/k8s-add-container1.png" alt="Add Container">

  <li>Click in the field <b>Select Container</b> to select the container from the list of available containers.</li>

  <img src="images/k8s-select-container-t1.png" alt="Add Container">

  <li>Click in the field <b>Enter Tag</b> to enter a static tag. <b>-OR-</b> You can set a regex that will match tags, by clicking in the field <b>Enter Regex</b> and entering a tag matching regex.</li>

  <img src="images/k8s-select-tag1.png" alt="Select Tag">

  <b>-OR-</b>

  <img src="images/k8s-select-tag2.png" alt="Select Tag">

  <li>When you are ready, click the <b>Save Source</b> button.</li>
</ol>

## Add a deployment to a pipeline

> **Note:** Before a deployment can be added to a pipeline, a deployment must first be created. 

There are several ways you can configure deployments in the pipeline. You can add a deployment to an existing stage to run concurrently with an existing job, you can add a deployment in its own stage, or run multiple deployments concurrently in a stage.

<ol>
  <li>While viewing a pipeline, click the <b>+ Add Deployment</b> link to add a concurrent deployment to deploy in an existing stage,  or click the <b>Add Deployment Stage</b> button to add a new stage for the deployment.</li>

  <img src="images/job-pipeline1.png" alt="Add Deployment">

  <li>Select the <b>cluster</b> where the deployment exists.</li>
  <li>Select the <b>namespace</b> where the deployment exists.</li>
  <li>Select the <b>deployment</b> from the list of available existing deployments.</li>

  <li>Configure your <b>Container Mapping</b> as necessary. For more info, see <a href="./alias-map.html">Alias Single Image to Multiple Containers</a>.</li>
  <li>Click the <b>Add Stage</b> button.</li>
</ol>

You have added a deployment to your pipeline.

Realize you can add more than one deployment to a pipeline.

<img src="images/job-pipeline2.png" alt="Add Deployment">

In the above example:

<ol>
  <li>When a build of any container in the pipeline completes successfully, the pipeline is initiated.</li>
  <li>The <b>k8s-mysql</b> deployment is seployed after successful build. When this is successful, the pipeline will continue.</li>
  <li>The <b>db-migrate</b> deployment will be dispatched after the deploy above is successful.</li>
  <li>After the db-migrate deployment is successful, the <b>start-timer</b> deployment will be dispatched at the same time (concurrently) the <b>k8s-wordpress</b> is deployed.</li>
</ol>

## Add a job to a pipeline

> **Note:** Before a job can be added to a pipeline, a job template must first be created. For more info, see <a href="./job.html">Create a Job</a>.


<h3>Add a Job to a Pipeline</h3>

There are several ways you can dispatch jobs in the pipeline. You can add a job to an existing stage to dispatch concurrently with a deployment, you can add a job as its own stage, or dispatch multiple jobs concurrently in a stage.

<ol>
  <li>While viewing a pipeline, click the <b>+ Add Job</b> link to add a concurrent job to an existing stage, or click the <b>Add Job Stage</b> button to add a new stage for the job.</li>

  <img src="images/job-pipeline1.png" alt="Add Job">

  <li>Select the job from the list of available existing job templates.</li>

  <p>A default cluster and/or namespace may already be specified in the job template. You can choose a different cluster/namespace to dispatch this job to during pipeline execution.</p>

  <li>Validate or change the <b>Cluster</b> and <b>Namespace</b>.</li>
  <li>Click the <b>Add Stage</b> button.</li>
</ol>

You have added a job to your pipeline.

Realize you can add more than one job to a pipeline.

<img src="images/job-pipeline2.png" alt="Add Job">

In the above example:

<ol>
  <li>When a build of any container in the pipeline completes successfully, the pipeline is initiated.</li>
  <li>The <b>k8s-mysql</b> deployment is deployed after successful build. When this deploy is successful, the pipeline will continue.</li>
  <li>The <b>db-migrate</b> job will be dispatched after the deploy above is successful.</li>
  <li>After the db-migrate job is successful, the <b>start-timer</b> job will be dispatched at the same time (concurrently) the <b>k8s-wordpress</b> is deployed.</li>
</ol>

## Set auto-build in a pipeline

Pipelines auto build provides for continuous integration. This means developers can simply check-in code and Pipelines can auto-build (and auto-deploy) that code.

After adding a container to a pipeline, you can set the container auto-build options.

> **Note:** Auto Build options are branch specific.

<ol>
  <li>While viewing a pipeline, click the text <b>Auto Build</b> for the container you wish to set auto-build options.</li>

  <img src="images/k8s-set-auto-build1.png" alt="Auto Build">

  <p>You will be presented with 3 options. They are as follows:</p>

  <ul>
    <li><b>Commit</b> - Build this branch when a commit (push/merge) is done.</li>
    <li><b>PullRequest</b> - Build the branch making a PR against this branch.</li>
    <li><b>Tag</b> - Build this branch when it is tagged.</li>
  </ul>

  <img src="images/k8s-set-auto-build-triggers.png" alt="Auto Build Triggers">

  <li>Select the <b>Auto Build Triggers</b> you wish to use to trigger builds of this container branch.</li>
  <li>Click the <b>X</b> to close the dialog when you are finished.</li>
</ol>

In this scenario, when a user checks in code to the Master branch of Github repository doct15/k8s-mysql, it will be auto-built. If the build succeeds, the Kubernetes automation pipeline can be initiated.

## Set auto-polling in a pipeline

Pipelines auto polling provides for continuous integration of containers stored on a Docker registry. This means a simple <code>docker push</code> of a new container to a Docker registry can initiate a Kubernetes automation pipeline in Pipelines.

<h3>Set Auto-Polling</h3>

After adding a Docker registry container to a pipeline, you can enable the container auto-polling options.

> **Note:** Auto Polling is tag specific.

<ol>
  <li>While viewing a pipeline, click the text <b>Polling</b> for the container you wish to enable/disable auto-polling.</li>

  <img src="images/k8s-set-auto-polling1.png" alt="Auto Polling">

  <p>You will be presented with the ability to enable or disable polling.</p>

  <img src="images/k8s-set-auto-polling-triggers.png" alt="Auto Build Triggers">

  <li>Click the <b>X</b> to close the dialog when you are finished.</li>
</ol>

In the above scenario, if an image is <code>docker push</code> to the doct15/k8s-wordpress repository with a tag matching regex <code>[0-9]+</code>, it will initiate the Kubernetes pipeline automation when polling is enabled.

## Set auto-deploy in a pipeline

Pipelines auto deploy provides for continuous deployment. This means developers can simply check-in code and Pipelines can auto-build and auto-deploy that code.

> **Note:** Before auto-deploy can be configured a Kubernetes deployment specification must first be created. For more info see <a href="./project.html">Create a K8S Deployment</a>

<h3>Set Auto-Deploy</h3>

<ol>
  <li>In a project pipeline that has already existing containers, click the <b>Add Stage</b> button.</li>
  <li>Select the <b>Cluster</b> you wish to deploy to.</li>
  <li>Select <b>Cluster Namespace</b>.</li>
  <li>Click in the <b>Search by namespace or name...</b> field.</li>
  <li>Select the deployment specification created earlier.</li>

  <img src="images/k8s-add-stage-dialog.png" alt="Add Stage">

  <li>Click the <b>Deployment</b>.</li>
  <li>Ensure the containers in your deployment spec are all mapped to containers in your project. For more information on how to use container mapping see <a href="./alias-map.html">Alias Single Image to Multiple Containers</a>.</li>

  <img src="images/k8s-container-mapping.png" alt="Container Mapping">

  <li>Click the <b>Add Stage</b> button.</li>
  <li>Click <b>Close</b> to close the dialog.</li>
  <li>Now click (enable) the <b>Auto Deploy on Build Success</b> option.</li>

  <img src="images/k8s-auto-deploy-on-build-success.png" alt="Auto Deploy on Build Success">

</ol>

The above pipeline depicts the following; If either the k8s-mysql or k8s-wordpress containers successfully build, an auto-deploy to the wordpress deployment will occur. This deployment will deploy both containers.

<h3><a name="add-a-deployment-stage"></a>Add a Deployment Stage</h3>

The project pipeline deploy automation can deploy to clusters across any cloud or vendor. In the below illustration note that after <b>Any Deploy Success</b> of the k8s-wordpress or k8s-mysql, a further automated deployment is done to a different cluster (sam-cluster).

<img src="images/k8s-pipeline-chain.png" alt="Pipeline Chain">


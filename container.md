---
layout: default
title: "Containers"
---

Pipelines automates the building and deploying of docker containers to Kubernetes.

Containers, in Pipelines, refers to Docker containers. If not deployed (running), the term "containers" may refer to a Docker image.

<img src="images/k8s-3-containers-info2.png" alt="containers info">

> **Note:** Containers that are not attached to a software repository do not have <i>Build Instructions</i> as an option.

## Add containers

Once you have created a project, in Pipelines, you can add containers to the project. These containers can come from a repository or a docker registry image.

If you choose to add a container from a repository, Pipelines can build the containers. Builds can be automated.

Any container added can be deployed to a cluster.

Before adding any containers, ensure <a href="./integrate.html">Integrations</a> are set up.


<h3>Add a Container</h3>

<h4>Step 1. Navigate to Project</h4>

Ensure you are on the project you wish to add a container to. You can navigate to your list of projects by clicking <b>Project</b> at the top left.

<img src="images/k8s-project-list.png" alt="Select Projects">

Click on your <b>Project</b> to navigate.

<img src="images/k8s-myproject.png" alt="MyProject">


<h4>Step 2. Add Container</h4>

Click the <b>Add Containers</b> button.

<img src="images/k8s-container-types.png" alt="Add Container types">

You will be presented with two options:
<ul>
  <li><b>Connect Source Control</b> - When you connect a container with Source Control, you are connecting a repository that will have code to build a docker image (precursor to a docker container). This repository must, at a minimum, have a Dockerfile that specifies how to build the image.</li>
  <li><b>Specify Registry</b> - When you connect a Docker Registry, you are accessing a previously built image from the registry. This image can be built from many other sources, including Pipelines.</li>
</ul>


<h5><a name="connect-source-control"></a>Connect Source Control</h5>

When connecting a docker container from source control, the following info must be supplied:

<img src="images/k8s-connect-source-control.png" alt="Connect Source Control">

The fields in that UI are as follows:

<ul>
  <li><b>Container Name</b> - The name of the container to be used in Pipelines.</li>
  <li><b>Source Control</b> - The software source control repository.</li>
  <li><b>Repository</b> - The name of the repository.</li>
  <li><b>Cloud Provider</b> - The docker registry cloud provider. You will be presented with a list of providers when selecting this field.</li>
  <li><b>Image</b> - The fully qualified name of the image. This syntax differs by registry.</li>
</ul>




<h5><a name="specify-registry"></a>Specify Registry</h5>

When specifying a docker container from a registry, the following info must be supplied:

<img src="images/k8s-specify-registry.png" alt="Specify Registry">

The fields in that UI are as follows:

<ul>
  <li><b>Container Name</b> - The name of the container to be used in Pipelines.</li>
  <li><b>Cloud Provider</b> - The docker registry cloud provider. You will be presented with a list of providers when selecting this field.</li>
  <li><b>Image</b> - The fully qualified name of the image. This syntax differs by registry.</li>
</ul>

After adding your containers, you will see your container(s) listed on the right of the project page.

<img src="images/k8s-3-containers-added.png" alt="Containers">

In the above example there are three containers.

<ul>
  <li><b>example</b> - A container from Dockerhub registry.</li>
  <li><b>k8s-mysql</b> - A container from a Github repository.</li>
  <li><b>k8s-wordpress</b> - A container from a Github reposotiry.</li>
</ul>

## Edit container

Once you have container(s) in a project you can edit, set build instructions, and delete them.

<h3>Edit a Container</h3>

<img src="images/k8s-3-containers-info2.png" alt="containers info">

Clicking the <b>Edit Container</b> icon will bring up the original source control or docker registry information for the container.

<h5><a name="connect-source-control"></a>Connect Source Control</h5>

When editing a docker container from source control, the following info may be edited:

<img src="images/k8s-connect-source-control2.png" alt="Connect Source Control">

The fields in that UI are as follows:

<ul>
  <li><b>Source Control</b> - The software source control repository.</li>
  <li><b>Repository</b> - The name of the repository.</li>
  <li><b>Cloud Provider</b> - The docker registry cloud provider. You will be presented with a list of providers when selecting this field.</li>
  <li><b>Image</b> - The fully qualified name of the image. This syntax differs by registry.</li>
</ul>


<h5><a name="specify-registry"></a>Specify Registry</h5>

When editing a docker container from a registry, the following info may be edited:

<img src="images/k8s-specify-registry2.png" alt="Specify Registry">

The fields in that UI are as follows:

<ul>
  <li><b>Cloud Provider</b> - The docker registry cloud provider. You will be presented with a list of providers when selecting this field.</li>
  <li><b>Image</b> - The fully qualified name of the image. This syntax differs by registry.</li>
</ul>

When done editing, click <b>Save Changes</b>.

## Build instructions

Once you have container(s) in a project you can edit, set build instructions, and delete them.

<h3>Container Build Instructions</h3>

<img src="images/k8s-3-containers-info2.png" alt="containers info">

Clicking the <b>Build Instructions</b> icon will bring up the build instructions and build options for the container.

<img src="images/k8s-build-instructions1.png" alt="build instructions">

<ul>
  <li><b>Build</b> - The code to build and test the container.</li>
  <li><b>Dockerfile Path</b> - The path to the Dockerfile in the repository..</li>
  <li><b>Build Hardware</b> - Select whether this should be built on shared build hardware in a docker container, or built on a private build server.</li>
  <li><b>Build Images</b> - If building on shared hardware, select the "flavor" of docker container to build in.</li>
  <li><b>Build Variables</b> - Enter any build environment variables that are required.</li>
</ul>

When complete, click <b>Save</b>.

The build instructions are automatically generated and inserted. The default build instructions are:

~~~
### Docker Build Commands ###
docker login -u "$DISTELLI_DOCKER_USERNAME" -p "$DISTELLI_DOCKER_PW" "$DISTELLI_DOCKER_ENDPOINT"
docker build --quiet=false -t "$DISTELLI_DOCKER_REPO" "$DISTELLI_DOCKER_PATH"
docker tag "$DISTELLI_DOCKER_REPO" "$DISTELLI_DOCKER_REPO:$DISTELLI_BUILDNUM"
docker push "$DISTELLI_DOCKER_REPO:$DISTELLI_BUILDNUM"
### End Docker Build Commands ###
~~~

## Delete container

Once you have container(s) in a project you can edit, set build instructions, and delete them.

<h3>Delete a Container</h3>

<img src="images/k8s-3-containers-info2.png" alt="containers info">

Clicking the <b>Delete Container</b> icon (trash can) will allow you to delete the container from the project.

<img src="images/k8s-delete-container.png" alt="Delete Container">

Click the red <b>Delete</b> button when you are ready to delete or <b>Cancel</b> to cancel this operation.

## Build containers in a project

Once you have container(s) in a project you can edit, build, and delete them.

<h3>Build a Container</h3>

<img src="images/k8s-build-icon.png" alt="Build icon">

Clicking the <b>Build</b> icon will bring up a list of available containers in this project. Remember, containers that are connected to a Docker registry are not build-able.

<img src="images/k8s-build-container.png" alt="Build container">

Click the container that will be built. This will bring up a list of available branches.

<img src="images/k8s-build-branch.png" alt="Build branch">

Click (select) the <b>branch</b> that will be built.

Now click <b>Build</b>.

Your build will now begin.





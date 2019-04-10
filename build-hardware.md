---
layout: default
title: "Build hardware"
---

When building software with Pipelines, you can opt to build on Pipelines shared hardware or on your private hardware. This includes building images (containers) for Kubernetes deployments.

## Build Shared Hardware

When building on Pipelines shared hardware, you must select a docker image to build in.

<img src="images/k8s-build-shared-hardware.png" alt="Build Images">

Note, you can build an image with Pipelines and make it available in that list of images. For more info see [Creating Docker Build Image](./docker-build-image.html).

## Use your own build server

When building your application with Pipelines you can specify Pipelines to use your own build servers wherever they may exist. Once you have followed those steps and installed the Pipelines agent, your server will be available in the <b>Build Hardware</b> section of Pipelines for Containers.

<h3><a name="step-1.-install-the-distelli-agent"></a>Step 1. Install the Pipelines Agent</h3>

To correctly function as a build server in Pipelines you must first install the Pipelines agent on the build server.

Instructions for installing the Pipelines agent can be found here [Installing the Agent](./agent.html).

> **Caution:** For build server functionality, the server must be running Pipelines agent version 3.50 or greater. To see your Pipelines agent version see [the `agent version` command](./agent-command.html).

<h3><a name="step-2.-install-repository-client"></a>Step 2. Install Repository Client</h3>

For your build server to be able to retrieve software code from a repository, the appropriate client software must be installed.

> **Note:** Ensure you install the command line version. With Windows ensure you install the windows command prompt version.

Use [**git**](https://git-scm.com/downloads) for BitBucket, GitHub, and GitHub Enterprise.

For more information on installing Git for Windows, please see [Installing Git for Windows Build](../for-apps/build-configure.html).

Use [mercurial](https://www.mercurial-scm.org/downloads) for BitBucket.

<h3><a name="step-3.-mark-server-as-build-server"></a>Step 3. Mark Server as Build Server</h3>

From the Pipelines web UI you mark the server as a build server.

> **Note:** A server marked as a build server can still consume deployments from Pipelines.

<ol>
<li>In the Pipelines web UI click the <b>Servers</b> link from the top.</li>
<li>In the server list find the server you wish to make a build server and click the server name.</li>
<li>On the server page click the <b>Build Server</b> link in the top right.</li>
<li>In the resulting dialog box, click the <b>Enable</b> button.</li>
</ol>

You have enabled this server to build your applications. For more information see [Setting Build Server Capabilities](../for-apps/build-configure.html).

<h3><a name="step-4.-enable-application-to-use-build-server"></a>Step 4(VM). Enable Application to use Build Server</h3>

> **Note:** This section is specific to using the build server with the Pipelines VM Dashboard. Please skip to the next section for using the build server with Pipelines for Containers.

For an application to use a build server it must be integrated with a repository. To integrate your application with a repository see:

* [Connecting a Repository to an Application](../for-apps/application-manage.html).
* [Creating an Application from a Repository](../for-apps/application-create.html).

> **Note:** If your application is not integrated with a repository, this option will not be available.

To enable an application to use a build server:

1. [Navigate to the Application](../for-apps/application-manage.html)
1. Ensure you are on the **Overview** tab.
1. On the right click the **Build Options gear**.

    A dialog box will appear on the right.

1. Click the **Build on my own hardware** option at the top right.
1. Click the **Save** button.

You have enabled this application to build on your build servers. For more information see [Setting Build Server Capabilities](../for-apps/build-configure.html).

## How Pipelines for Containers queues builds

Pipelines allows users to build on Pipelines shared build servers and on private build servers. This document discusses those scenarios in more technical depth and how the queuing of builds is processed.

### Building on Shared Pipelines Build Servers

When building on Pipelines shared build servers, builds are done in Docker containers.
Each container has differing software installed to accomodate the builds of different languages.

The following containers are available to build:
<ul>
<li>Pipelines Haskell (Docker)</li>
<li>Pipelines Javascript (Docker)</li>
<li>Pipelines Java/JVM (Docker)</li>
<li>Pipelines Python (Docker)</li>
<li>Pipelines Perl (Docker)</li>
<li>Pipelines Ruby (Docker)</li>
<li>Pipelines Go (Docker)</li>
<li>Pipelines Base (Docker)</li>
<li>Pipelines PHP (Docker)</li>
<li>Pipelines Android (Docker)</li>
<li>Pipelines Legacy (Docker)</li>
</ul>

Documentation on the containers can be found here: [Pipelines Build Environments](./build-environment.html).

When building on Pipelines shared build servers, the Docker image selected is initiated as a running container. The build then takes place inside of this running container. This provides a pristine environment for each build. When the build is done, the container is destroyed.

### Build Queuing

Builds are queued by Application/Branch.

For example, if I have an application in Pipelines, tied to my repository and am actively building from commits to the <b>Master</b> branch; 3 consequtive commits to the <b>Master</b> branch will cause 3 build tasks to be scheduled. These will be processed on a first-come first-serve basis and will not run in parallel because they are for the same branch.

If instead I am actively building from commits to multiple branches (i.e. branch; Dev1, Feature1, Feature2) and three commits occur, one to each branch, at the same time; Pipelines will build all three branches at the same time (in parallel).

### Building on Private Build Servers

When building on private servers with Pipelines, builds are executed, by the agent, on your hardware. A build instructs the Pipelines agent to clone the repository/branch and run the build (PreBuild, Build, AfterBuildSuccess, etc...) steps as indicated in the distelli-manifest.yml. This is typically not done in a Docker container.

For more information on the Pipelines manifest build steps, see [Pipelines Manifest](../for-apps/manifest.html).

Each build is executed in its own unique Directory. When the build completes, the directory is removed.

The queuing of the builds on private build servers is the same schema as queuing on the shared build servers. On private build servers the builds are typically not running in docker containers which means parallel builds can affect each other.






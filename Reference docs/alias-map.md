---
layout: default
title: "Alias an image to multiple containers"
---

The container alias mapping feature allows you to automate deployments of the same image to multiple containers. To exemplify, consider this example:

A user has created a single docker image that includes all services, including: Web server, proxy, and content. The users wishes to run the same image as multiple containers, broken up into their respective services. Web server, proxy, and content. Each container will be started with differing options appropriate to start their service.

Here is an example Kubernetes deployment specification the user might use.

~~~
  apiVersion: extensions/v1beta1
  kind: Deployment
  metadata:
    name: example-app
    namespace: default
  spec:
    revisionHistoryLimit: 3
    minReadySeconds: 10
    strategy:
      type: RollingUpdate
      rollingUpdate:
        maxUnavailable: 1
        maxSurge: 1
    replicas: 1
    template:
      metadata:
        labels:
          app: example-app
      spec:
        containers:
        - name: website
          image: example/my-image:111111
          command: ["start_apache.sh"]
          args: ["HOSTNAME", "KUBERNETES_PORT"]
        - name: proxy
          image: example/my-image:111111
          ports:
          - containerPort: 8000
            hostPort: 80
            protocol: TCP
            name: nginx
          command: ["start_nginx.sh"]
          args: ["USERKEY"]
        - name: content
          image: example/my-image:111111
          command: ["start_content.sh"]
          args: ["CONTENT_DIR"]
~~~

As you can see above, there are 3 containers in this deployment that all use the same image <code>example/my-image</code>. Please note the tag <code>:111111</code>. Pipelines dynamically updates the tag with a Pipelines globally unique identifier during build and kubernetes deployment.

For Pipelines to accurately update this spec and dynamically update the image tag, you must alias (map) the deployment containers to the image (Pipelines container).

<h3>How to alias a container</h3>

First, add a container to a project in Pipelines. For more information on creating a project, please see <a href="./project.html">Create Project</a>.

<ol>
  <li>In your project, click the <b>Add Container</b> link.</li>
  <li>Click the <b>Connect Source Control</b> button.</li>
  <li>Fill in the appropriate values. The below represents the example noted above:</li>

  <img src="images/k8salias-container1.png " alt="k8s alias container">

  <p>Above a Pipelines container is being added representing image <code>example/my-image</code>. Pipelines can automate builds and kubernetes deployments of the container. For more information see <a href="./container-pipeline.html">Set Auto Build in a Pipeline</a> and <a href="./container-pipeline.html">Set Auto Deploy in a Pipeline</a>.</p>

  <li>Click <b>Add Container</b> to save the container. For more information on adding containers see <a href="./container.html">Add Containers to a Project</a>.</li>
  <li>Click <b>Close</b>.</li>

  <p>You should see the container added in the list on the right.</p>
  <p>Next you will have to create the deployment specification to add it as a stage to your pipeline.</p>

  <li>Click the <b>rocket</b> deployment icon on the top right.</li>

  <img src="images/k8s-deploy-icon-rocket.png" alt="k8s deploy rocket">

  <li>Select your <b>Cluster</b>.</li>
  <li>Click <b>Create a new deployment</b>.</li>
  <li>Paste in your kubernetes deployment <b>YAML</b>.</li>

  <img src="images/k8salias-deploy-yaml1.png" alt="k8s deploy yaml">

  <p>You will have to initiate a deployment to save this deployment specification.</p>

  <li>Enter a required <b>deployment Description</b>.</li>
  <li>Click <b>Deploy</b>.</li>

  <p>Your deployment is now beginning.</p>

  <li>Click the <b>X</b> at the top right to close the Deploy window.</li>

  <li>Click the <b>Pipelines</b> tab.</li>
  <li>Create a pipeline and add the container, created above, to the pipeline. For more information on creating pipelines see <a href="./container-pipeline.html">Create a Pipeline</a>. For more information on adding containers to pipelines see <a href="./container-pipeline.html">Add Container to a Pipeline</a>.</li>

  <li>After adding the container to the pipeline, click the <b>Add Stage</b> button in the pipeline.</li>

  <li>Select the <b>Cluster</b> where the deployment specification was deployed to.</li>
  <li>Select the <b>Namespace</b> where the deployment specificaiton was deployed to.</li>
  <li>Select the <b>deployment</b>.</li>

  <p>Note at the bottom, you will see a <b>Container Mapping</b> section.</p>

  <li>Click <b>Do not map to Project container</b> for the first container <b>proxy</b>.</li>

  <img src="images/k8salias-alias-container1.png " alt="k8s alias container">

  <p>This is where you select which <b>Project container</b> to map each of these <b>Kubernetes containers</b>.</p>

  <li>For each <b>Kubernetes containers</b> map the <b>Project container</b> <b>example-app</b> (which represents image <code>exampe/my-image</code>).</li>
  <li>Click <b>Add Stage</b> to save the stage.</li>
  <li>Click <b>Close</b>.</li>
</ol>

<img src="images/k8salias-pipeline-stage1.png" alt="k8s pipeline stage alias">

When you are done, you will see the container mappings in the pipeline stage as depicted above.

Now, whenever image <b>example/my-image</b> (Pipelines container example-app) is successfully built by Pipelines, the created stage can auto-deploy the new image to all three kubernetes containers.









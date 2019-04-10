---
layout: default
title: "Release Notes"
--- 

New features, enhancements, known issues, and resolved issues for the Pipelines for Containers 3.x release series.

## Version 3.2.0-NEXT

Release Target 20 August 2018

New in this release
* **Trigger customer Helm Chart builds on source changes in Pipelines**. Add custom Helm Charts from source control to Pipelines and build automatically as source changes.

Resolved in this release:
* Adding search filters on branch selection for container builds caused the branch list to be hidden.

## Version 3.1.0-431790

Released 31 July 2018

New in this release:

* **Build and deploy your own custom Helm Charts from source**. In addition to deploying Helm Charts from public repos, you can now build and deploy your own custom Charts. 

## Version 3.0.23-426036

Released July 19 2018

New in this release:

* Removed Distelli branding across the user interface. 
* When connecting to an RBAC-enabled K8s cluster, you’re now prompted to set the correct cluster permissions.
* Docker Hub credentials are now validated when you add a new container.

## Known issues

**Renamed required status check for protected branches in GitHub and GitHub Enteprise**
As part of our rebranding efforts, we renamed a required status check for protected branches in GitHub and GitHub Enterprise. Users of protected branches who have enabled this required status check must follow the instructions below to switch to the new status check. 

To fix this issue: 

1. In the GitHub or GitHub enterprise web UI, go to your repository's **Settings** and click **Branches**, then click **Edit** next to your protected branch.
1. In the status checks area, deselect **continuous-integration/distelli** and select **continuous-integration/puppet**, then save your changes. 
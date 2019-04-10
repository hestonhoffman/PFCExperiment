---
layout: default
title: "The Pipelines agent"
--- 

The Pipelines agent runs on your servers. The Pipelines agent software provides several pieces of functionality, including:

* [Pipelines CLI](./cli.html)
* [Pipelines deploys](./agent.html)
* [Private builds](./build-hardware.html)
* [Key management server](../for-apps/application-secure.html)

Pipelines uses an agent model to provide server communication. The Pipelines agent can be installed on any server in any network, cloud, or provider. The agent supports the following operating systems:

<ul>
<li>Linux</li>
<li>Mac</li>
<li>Windows</li>
</ul>

Upon installing and authenticating the Pipelines agent, the agent will make an encrypted connection back to the Pipelines SaaS. This simplifies providing access to servers from Puppet Pipelines. No need for SSH key management.

Within Pipelines you can [provision EC2 instances](../for-apps/server-type.html) that will auto-install the Pipelines agent.

[Automated install and authentication](./distelliyml.html) of the agent is simple and can be done on any server in any network, cloud, or provider.

## Installing the Pipelines agent

The Pipelines agent connects your destination server to Pipelines for consuming application deployments. The agent is also required if you will be using Puppet Pipelines to build on your own servers. For more info see [Using your own Build Server](./build-hardware.html).
To install the agent on your destination server, run the command below that is appropriate for your server's OS.

> **Note:** This installation requires root (administrator) permissions.

<h3><a name="linux-and-mac-os-x"></a>Linux and macOS X</h3>

To install on Linux or macOS X you can use either curl <b>or</b> wget with one of the following syntaxes.
<h4>wget example</h4>

~~~
wget -qO- https://www.distelli.com/download/client | sh
~~~

<h4>curl example</h4>

~~~
curl -sSL https://www.distelli.com/download/client | sh
~~~

<h3><a name="windows"></a>Windows</h3>

To install on Windows, copy and paste the following PowerShell command into a command (cmd) window.

~~~
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://www.distelli.com/download/client.ps1'))" & SET PATH=%PATH%;%ProgramFiles%/Distelli
~~~

<h3><a name="complete-the-install"></a>Complete the Install</h3>

You now have the Pipelines CLI installed. To complete the install of the agent, you must issue the `/usr/local/bin/distelli agent install` command.

~~~
/usr/local/bin/distelli agent install
~~~

~~~
ServerA:~$ <b>wget -qO- https://www.distelli.com/download/client | sh</b>
This script requires superuser privileges to install packages
Please enter your password at the sudo prompt

[sudo] password for bmcgehee: 
    Installing Distelli CLI 3.51 for architecture 'Linux-x86_64'...
    Downloading https://s3.amazonaws.com/download.distelli.com/distelli.Linux-x86_64/distelli.Linux-x86_64-3.51.gz
To install the agent, run:
    sudo /usr/local/bin/distelli agent install
ServerA:~$ <b>sudo /usr/local/bin/distelli agent install</b>
Distelli Email: jdoe@distelli.com
      Password: 
    1: User: jdoe
    2: Team: janedoe/TeamJane
Team [2]: <b>1</b>
Server Info: https://www.distelli.com/jdoe/servers/12345678-4765-ac42-bd7a-080027c8277c
Starting upstart daemon with name:	dtk-supervise-cc123456787ad94a8d34ac610381242f9ae28bb8
~~~

<h3><a name="verify-the-install"></a>Verify the install</h3>

To validate the agent is installed and working use the `/usr/local/bin/distelli agent status` command.

> **Note:** This command requires root (administrator) access.

~~~
/usr/local/bin/distelli agent status
Distelli Agent (serverA) is Running with id 766b88c8-e925-11e4-ae8b-080027cc07f7
~~~

<h3><a name="installation-options"></a>Installation options</h3>

Install and possibly start (or restart) the agent.

<h2>SYNTAX</h2>


~~~
/usr/local/bin/distelli agent install [-nostart] [-onboot] [-conf FILE]
~~~


<h2>OPTIONS</h2>

~~~
-nostart
~~~

This will install the agent, but not start it. Manual action will be required to start the agent.

~~~
-onboot
~~~

This will install the agent, but not start it. The agent will automatically start after the next reboot.

~~~
-conf FILE
~~~


This option tells the agent to read a distelli.yml for the agent access token and secret key. See the [distelli.yml usage guide](./distelliyml.html) for more information.

<h2>USAGE</h2>


The `/usr/local/bin/distelli agent install` command can be used to change the agent behavior. Using this command you can specify install options, as noted above.
If you issue this command on a server that has running deployed software, it will continue to run. If you specify the `-nostart` option, the applications will not continue to run after a boot of the server. Doing a `/usr/local/bin/distelli agent install` or `/usr/local/bin/distelli agent start` will (re)start the deployed applications.

> **Note:** The above comments assume the application running was started with the [Exec section of the distelli-manifest.yml](../for-apps/manifest.html).


<h2>EXAMPLES</h2>

Reinstall the agent and tell it not to start until next boot.

~~~
/usr/local/bin/distelli agent install -onboot
~~~


<h3><a name="upgrading-the-agent"></a>Upgrading the Agent</h3>

To upgrade the Pipelines agent, simply re-install the agent on top of the existing agent. This will perform an upgrade.

> **Note:** During the upgrade you can specify [install options](#installation-options).


<h3><a name="install-a-specific-agent-version"></a>Install a Specific Agent Version</h3>

You can install earlier versions of the Pipelines agent with one of the following syntaxes.

<h4>wget syntax</h4>

~~~
wget -qO- https://www.distelli.com/download/client/#.##.## | sh
~~~

<h4>curl syntax</h4>

~~~
curl -sSL https://www.distelli.com/download/client/#.##.## | sh
~~~

<h4>Example</h4>

~~~
curl -sSL https://www.distelli.com/download/client/3.62.14 | sh
~~~

<h4>Windows</h4>

~~~
powershell -NoProfile -ExecutionPolicy Bypass -Command "iex ((new-object net.webclient).DownloadString('https://www.distelli.com/download/client/#.##.##.ps1'))" & SET PATH=%PATH%;%ProgramFiles%/Distelli
~~~

<h3><a name="install-the-agent-non-sudo"></a>Install the agent non sudo</h3>

By default, the Pipelines agent will want to use sudo to install itself. You can install the agent without sudo. It's important to note, however, that if you do this, users doing Pipelines builds, restarts, terminate, and/or deploy tasks on the server will not have access to run sudo commands.

Here are the steps to install the Pipelines agent without sudo:

1. Create a user for the Pipelines agent to run as.

	In a normal install, this user defaults to <b>distelli</b>.

	~~~
	useradd -m distelli
	~~~

	You can change the user name to whatever you like, but this document will continue to refer to the user as "distelli".

1. Create a directory for the Pipelines agent executable.

	This directory will house the "distelli" agent executables. If you wish users to have access to this command, you may want to add this to the path.

	The distelli user must have write access to this directory.

	~~~
	mkdir /home/distelli/bin
	~~~

	In a normal install, this defaults to <b>/usr/local/bin</b>.

1. Set the Pipelines agent Executable Directory Environment Variable

	Setting this tells the install script where to place the executable. This directory was created in the previous step.

	~~~
	export DISTELLI_INSTALL_DIR=/home/distelli/bin
	~~~

	In a normal install, this is unnecessary.

1. Add a Working Directory for Pipelines to do Builds and Deploys

	This is the directory that the Pipelines agent will use for executing builds, deploys, and logging.

	The distelli user must own this directory.

	~~~
	mkdir /home/distelli/distelli
	~~~

	The unix owner of this directory will be the user that the Pipelines agent runs as.

	In a normal install, this directory is <b>/distelli</b>.

1. Add a Directory for Startup Scripts

	The Pipelines agent needs to be automatically started on server reboot. If you are installing the agent without sudo access, you will need to manually update the servers init scripts from these.

	The Distelli user must have write access to this directory.

	Create a directory for Pipelines to create the init scripts in.

	~~~
	mkdir /home/distelli/sysv
	~~~

1. Swith User to the distelli User

	To run the Pipelines agent install, use the distelli user. Either log out and login as this user, or <b>su</b> (Switch User) to the user.

	~~~
	su - distelli
	~~~

1. Download the Pipelines Agent Install Script

	In this step you will download the install script. This script is dependent on the environment variable DISTELLI_INSTALL_DIR, set above. If you just logged in as the Distelli user, you will have to re-set the DISTELLI_INSTALL_DIR environment variable.

	~~~
	wget -qO- https://www.distelli.com/download/client | sh
	~~~

	If you are prompted for sudo access in the above command, this is typically a permissions issue that the distelli user doesn't have permission to the directory DISTELLI_INSTALL_DIR or the environment variable is not set.

1. Install the Agent

	When installing the agent, you will have to specify directories created above as options in the command. Here is an example:

	~~~
	/home/distelli/bin/distelli agent install -data-dir /home/distelli/distelli -manager sysv -manager-dir /home/distelli/sysv
	~~~

1. Copy the init Scripts

	Finally you should look in the /home/distelli/sysv directory for the server init scripts. These scripts need to be moved to their appropriate place so that when the server reboots, the Pipelines agent is restarted.

## Automate the installation of the Pipelines agent

You can automate installation of the Pipelines agent using a distelli.yml configuration file. For more information on the distelli.yml see [distelli.yml Usage](./distelliyml.html).

<h3><a name="distelliyml"></a>distelli.yml</h3>

The distelli.yml syntax options for automating agent installs are as follows:

~~~
DistelliAccessToken: 'DISTELLI_ACCESS_TOKEN'
DistelliSecretKey: 'DISTELLI_SECRET_KEY'
Environments:
  - ENV_NAME1
  - ENV_NAME2
~~~


<ul>
<li><b>DISTELLI_ACCESS_TOKEN</b> - The Pipelines agent access token. <i>See below on how to retrieve.</i></li>
<li><b>DISTELLI_SECRET_KEY</b> - The Pipelines agent secret key. <i>See below on how to retrieve.</i></li>
<li><b>ENV_NAME#</b> - The Pipelines application environment that the server should join. Note that the server will join these environments in order (top to bottom) and, if enabled, deploy the current active release.</li>
</ul>

These fields are tied to a Puppet Pipelines account. Ensure you are [using the correct accoun](./users.html) when retrieving these values.

<h4>Retrieving Credentials</h4>

<ol>
<li>Click the <b>gear</b> icon from the top right.</li>
<li>Click the <b>Agent</b> icon on the left.</li>
<li>Under <i>Secret Key</i> click the <b>Show</b> button.</li>
</ol>

Here you will find the agent's Access Token and Secret Key. Add them to the distelli.yml. For example:

~~~
DistelliAccessToken: '12345678901234567890123456'
DistelliSecretKey: '1234567890123456789012345678901234567'
~~~


<h3><a name="placing-the-file"></a>Placing the File</h3>

The default location for placing the distelli.yml file is <b>/etc</b>.

On Windows, the default location is <b>%SystemDrive%\distelli.yml</b>.

You can override the default location with the [`-conf` option](#installation-options).


<h3><a name="how-to"></a>How to</h3>

The following list outlines, from a high level, the steps to automate the install of the Pipelines agent. These are the steps your "tool" would need to take to when provisionining your server.

<ol>
<li>Write the distelli.yml file in the correct directory with the appropriate values.</li>
<li>Download the Pipelines agent install script and execute it.</li>
<li>Run the Pipelines agent install command.</li>
<li>Log in to the Pipelines CLI (for builds).</li>
</ol>

> **Note:** For the agent to complete installation in step 3, the system/server must have access to the network.

<h3><a name="user-data"></a>User Data</h3>

Many cloud computing platforms provide <b>user-data</b> when provisioning an instance. This is true of Amazon EC2 and Digital Ocean droplets. Below is a working example of EC2 user-data that will install the Pipelines agent on provisioning an EC2 instance. 

~~~
#!/bin/bash
echo "DistelliAccessToken: '12345678901234567890123456'" > /etc/distelli.yml
echo "DistelliSecretKey: '1234567890123456789012345678901234567'" >> /etc/distelli.yml
echo "Environments:" >> /etc/distelli.yml
echo "  - java_app_dev" >> /etc/distelli.yml
wget -qO- https://www.distelli.com/download/client | sh
/usr/local/bin/distelli agent install -conf /etc/distelli.yml
/usr/local/bin/distelli login -conf /etc/distelli.yml
~~~

## Automatic agent install on Amazon EC2 instances

<br>
While installing the agent manually is easy, there may be several cases where its desirable to have the agent installed automatically when a new instance is launched on Amazon EC2. In this guide, we'll walk through the steps required to configure the EC2 User Data so that the Pipelines agent is automatically installed when a new EC2 Instance is started. This can be especially useful when instances are started via AWS Auto Scaling.
Amazon EC2 allows you to specify shell scripts or commands in the User Data section, that run on your Linux instance at launch. To automatically install the agent on instance launch add the following commands to the User Data section of your launch configuration or in the AWS Console when launching a new instance:

~~~
#!/bin/bash

echo "
DistelliAccessToken: 'DISTELLI_ACCESS_TOKEN'
DistelliSecretKey: 'DISTELLI_SECRET_KEY'
" > /etc/distelli.yml

wget -qO- https://www.distelli.com/download/client | sh
/usr/local/bin/distelli agent install
~~~

The Pipelines Access Token and the Pipelines Secret Key register this agent with your Pipelines account. You can obtain your access token and secret key from your Pipelines Account by clicking <b>Settings () > Credentials > Agent Credentials</b>. The wget command installs the agent and starts it.
With the script in the User Data, section, launch your EC2 instance and it will automatically install the agent and start it. Once the agent is installed and running, the server will appear in your Pipelines Console under servers and you can add it to an environment and deploy your code to it.

<h3><a name="auto-deploy-from-an-environment"></a>Auto Deploy from an Environment</h3>

In addition to installing an agent on a new EC2 Instance, you can also specify a list of environments the new server should join and Pipelines will automatically add the server to those environments and deploy the correct release for the applications associated with those environments.
To specify the environments that the server should add itself to, add the Environments entry to the distelli.yml config file in the User Data. Here is a complete example:

~~~
#!/bin/bash

echo "
DistelliAccessToken: 'DISTELLI_ACCESS_TOKEN'
DistelliSecretKey: 'DISTELLI_SECRET_KEY'

Environments:
  - node-js-runtime-prod
  - app-dependencies-prod
  - web-server-prod
" > /etc/distelli.yml

wget -qO- https://www.distelli.com/download/client | sh
/usr/local/bin/distelli agent install
~~~

In the example above, we included the Environments section in the distelli.yml config file that specifies that this EC2 instance should be added to the three environments specified (node-js-runtime-prod, app-dependencies-prod and web-server-prod) in that order. Pipelines will then automatically start deployments from each environment in turn and wait for each deployment to complete before starting the next one.

Auto deployments deploy the active release associated with each environment. The active release is the last release deployed within that environment. If an environment has received no deployments, then the auto deployments will have no effect. To ensure that your auto deployments are successful, please ensure that the last deployment to an environment completes successfully.

## Automatic agent install with Chef

Installing the Pipelines agent can also be accomplished as part of a Chef bootstrap.

The following procedures assumes you have familiarity with Chef, have a login to [Chef Manage](https://api.chef.io/login), and have [a Pipelines account](https://pipelines.puppet.com/signup).

<h3><a name="download-the-cookbook"></a>Download the Cookbook</h3>

The cookbook and recipe for installing the Pipelines Agent with chef can be found in the github repository [here](https://github.com/Distelli/DistelliAgentCookbook). 

1. On the Chef server navigate to the cookbook directory.
1. Enter the following command to clone the DistelliAgentCookbook:

~~~
git clone https://github.com/Distelli/DistelliAgentCookbook.git
~~~

1. Rename the directory (cookbook).

~~~
mv DistelliAgentCookbook/ distelli
~~~

You have downloaded the Pipelines Agent Chef cookbook.

<h3><a name="create-a-chef-role"></a>Create a Chef Role</h3>

1. Create a role to run the Pipelines Agent installer recipe.

~~~
knife role create distelli_agent
~~~

> **Note:** You may have to set the EDITOR environment variable for the previous command.       For example:

    `export EDITOR=vi`

    Or simply provide the `--editor` option with the knife command.

    `knife role create distelli_agent --editor vi`

1. Enter the following information into the role.

~~~
{
  "name": "distelli_agent",
  "description": "",
  "json_class": "Chef::Role",
  "default_attributes": {
    <b>"distelli": {
      "agent": {
        "access_token": "DISTELLI_ACCESS_TOKEN",
        "secret_key": "DISTELLI_SECRET_KEY"
      }
    }</b>
  },
  "override_attributes": {

  },
  "chef_type": "role",
  "run_list": [
    <b>"recipe[distelli]"</b>
  ],
  "env_run_lists": {

  }
}
~~~

The <b>DISTELLI_ACCESS_TOKEN</b> and <b>DISTELLI_SECRET_KEY</b> fields are tied to a Pipelines account. 

> **Retrieving Credentials** 
   1. Click the <b>gear</b> icon from the top right of the Pipelines web UI.
   1. Click the <b>Agent</b> icon on the left.
   1. Under <i>Secret Key</i> click the <b>Show</b> button.

1. Save the above role.

You have created a role to run the Pipelines Agent cookbook.

<h3><a name="update-chef-manage-cookbooks"></a>Update Chef Manage Cookbooks</h3>

1. Update your cookbooks at Chef Manage.

~~~
knife cookbook upload distelli
~~~

You can now bootstrap a remote server to install the Pipelines Agent.


<h3><a name="running-the-chef-recipe-bootstrap"></a>Running the Chef Recipe Bootstrap</h3>


1. Run the knife bootstrap for role distelli_agent to install the agent on a new node.

~~~
knife bootstrap --run-list "role[distelli_agent]" --ssh-user root --ssh-password pa55w0rd 192.0.2.67
~~~


The agent is now installed, authenticated, and running on your server. If you navigate to your servers list in Pipelines, you will see the server.

<h3><a name="other-distelli-agent-install-options"></a>Other Pipelines Agent Install Options</h3>

You can further provide Pipelines Application Environments for the server to automatically join. If the environment has the [Automatically deploy the active release when a new Server joins this environment](../for-apps/environment.html) enabled, the the server will automatically consume a deployment of the active release.

When specifying environments for the Pipelines agent to join, realize that the order of the environments is relevant in that the server will join each environment in order, completing any deployments before joining the next environment, in order. There is a 30 second delay between each deployment.

The settings for this can be found in the Chef role created earlier. To edit the role, use the following command:

~~~
knife role edit distelli_agent
~~~

An example below shows the addition of three environments: test-dev, test-qa, and test-prod.

~~~
{
  "name": "distelli_agent",
  "description": "",
  "json_class": "Chef::Role",
  "default_attributes": {
    "distelli": {
      "agent": {
        "access_token": "DISTELLI_ACCESS_TOKEN",
        "secret_key": "DISTELLI_SECRET_KEY"<b>,
        "environments": [
          "test-dev",
          "test-qa",
          "test-prod"
        ]</b>
      }
    }
  },
  "override_attributes": {

  },
  "chef_type": "role",
  "run_list": [
    "recipe[distelli]"
  ],
  "env_run_lists": {

  }
}
~~~

> **Important:** Don't forget the comma at the end of the "secret key" line!

After making this change and saving the role, you can run the `chef-client` command, on your nodes, to have the new changes take effect.

## Automatic agent install with DigitalOcean

This tutorial will walk you through how to automatically install the Pipelines Agent and add your new Droplet to your specific environment using Digital Ocean's Droplet User Data.

### Prerequisites

To complete this tutorial you will need to have the following:

* [Pipelines Account](https://pipelines.puppet.com/signup)
* [Pipelines Application](../for-apps/application-create.html)
* [DigitalOcean Account](https://www.digitalocean.com)

## Step 1. Launch Your Droplet

To start login to your DigitalOcean account and click <b>Create Droplet</b> in the upper right hand corner.

<img src="images/NodeTutorial/createDigitalOceanDroplet.png" alt="Create New Digital Ocean Droplet" />

Select your <b>Image</b>, <b>Size</b>, and <b>Region</b>. In the <b>Additional Options</b> section check the box next to <b>User Data</b>

<img src="images/NodeTutorial/digitalOceanEnableUserData.png" alt="Digital Ocean enable user data" />

This will open a text area for you to enter in your <b>User Data</b>. To automate the install of the Pipelines Agent, use the script below:

~~~
#!/bin/bash

export DISTELLI_ACCESS_TOKEN='YOUR DISTELLI ACCESS TOKEN'
export DISTELLI_SECRET_KEY='YOUR DISTELLI SECRET KEY'

echo "DistelliAccessToken: $DISTELLI_ACCESS_TOKEN" > /etc/distelli.yml
echo "DistelliSecretKey: $DISTELLI_SECRET_KEY" >> /etc/distelli.yml
echo "Environments:" >> /etc/distelli.yml
echo "  - YOUR DISTELLI ENVIRONMENT" >> /etc/distelli.yml
apt-get -y install wget
wget -qO- https://www.distelli.com/download/client | sh
/usr/local/bin/distelli agent install -conf /etc/distelli.yml
/usr/local/bin/distelli login -conf /etc/distelli.yml
~~~

You will need to insert your own Pipelines <b>Access Token</b> and <b>Secret Key</b>. These fields are tied to a Pipelines account. 
<h4>Retrieving Credentials</h4>

<ol>
<li>Click the <b>gear</b> icon from the top right.</li>
<li>Click the <b>Agent</b> link on the left.</li>
<li>Under <i>Agent Credentials</i> click the <b>Show</b> button.</li>
</ol>

You will see your <b>Access Token</b> and <b>Secret Key</b> here. Please insert them into your <b>User Data</b> script, and insert the Pipelines environment you want to add your server to.

> **Caution:** If the environment setting "Auto Deploy the Active Release when a new Server joins this environment" is enabled (checked) and there is an active release, an auto deploy will occur when servers join an environment using distelli.yml.
For more info, see [Environment Settings](../for-apps/environment.html).

Once you have inserted your <b>Access Token</b>, <b>Secret Key</b>, and <b>Environment</b> into your <b>User Data</b> script you can finishing configuring your Droplet. Once you are done, launch your Droplet and the Pipelines agent will be automatically installed and added to your specified environment. After the Droplet has finished launching, navigate to your Pipelines environment to ensure your server was added successfully.

<img src="images/NodeTutorial/digitalOceanServerAddedSuccessfully.png" alt="Server Sucessfully added to Pipelines Environment" />


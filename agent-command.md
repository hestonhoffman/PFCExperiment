---
layout: default
title: "Agent commands"
---

**intro text goes here**

## <h3><a name="agent-dump"></a>/usr/local/bin/distelli agent dump</h3>

Prints the agent processes, deployed applications, and current deployments.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent dump
~~~

<h2>OPTIONS</h2>

none

<h2>USAGE</h2>

This command is typically used for troubleshooting or to quickly see what applications are deployed and running on the server.

<h2>EXAMPLES</h2>

~~~
/usr/local/bin/distelli agent dump
Processes:
DistelliAgent Running 1136 2015-07-08 13:14:01 PDT (3 hours ago)
envs/SA_Linux Running 13200 2015-07-08 16:40:11 PDT (2 minutes ago)

Apps:
d123:simpleapp:sa_linux Running /distelli/envs/SA_Linux/bin/distelli-run.sh Daemon
d-a123456789b123456789
a-c987654321d987654321
-1/10/900/900/900
~~~

## <h3><a name="agent-help"></a>/usr/local/bin/distelli agent help</h3>

Prints the agent commands and brief help message for each.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent help
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

Use to get help.

<h2>EXAMPLE</h2>

~~~
/usr/local/bin/distelli agent help
Usage: /usr/local/bin/distelli agent -dtk-dir <dir> <command>

Connect your server to Pipelines

-dtk-dir <dir>
Undocumented, defaults to /distelli

stop
Stops all processes being supervised, and stops the supervisor, use with CAUTION since all applications deployed (and the agent) will be stopped

version
Display the version of the agent

status
Check if the agent is running and print the server name

uninstall
Uninstall the Pipelines agent permanently.

run
Run the Pipelines agent in the foreground, printing log files to STDERR. This command should only be ran as a child of `dtk supervise`.

install
Install and possibly start (or restart) the agent.

dump
Print the processes, applications, and current deployments

loglevel debug|info|warn|error
Set the log level

start
Start (or restart) the agent.

supervise
Undocumented
~~~

## <h3><a name="agent-install"></a>/usr/local/bin/distelli agent install</h3>

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


This option tells the agent to read a distelli.yml for the agent access token and secret key. See [distelli.yml usage](./distelliyml.html) for more information.

<h2>USAGE</h2>


The `/usr/local/bin/distelli agent install` command can be used to change the agent behavior. Using this command you can specify install options, as noted above.
If you issue this command on a server that has running deployed software, it will continue to run. If you specify the -nostart option, the applications will not continue to run after a boot of the server. Doing a `/usr/local/bin/distelli agent install` or `/usr/local/bin/distelli agent start` will (re)start the deployed applications.

> **Caution:** The above comments assume the application running was started with the [Exec section of the distelli-manifest.yml](../for-apps/manifest.html).


<h2>EXAMPLES</h2>

Reinstall the agent and tell it not to start until next boot.

~~~
/usr/local/bin/distelli agent install -onboot
~~~

## <h3><a name="agent-loglevel"></a>/usr/local/bin/distelli agent loglevel</h3>

Set the agent logging level. Logging is done to /distelli/logs/agent.log. The default is **info**.

> **Caution:** This command is typically used only under the guidance of Puppet Pipelines support.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent loglevel debug|error|info|warn
~~~

<h2>OPTIONS</h2>


~~~
debug
~~~

Sets the logging level to debug. The highest level of logging.

~~~
error
~~~

Sets the logging level to error. The agent will only log errors.

~~~
info
~~~

Sets the logging level to info. The agent will log information messages that highlight progress. This is the default level.

~~~
warn
~~~

Sets the logging level to warn. Only potentially harmful situations will be logged.

<h2>USAGE</h2>

This command will typically only be used when requested by Puppet Pipelines support.

<h2>EXAMPLES</h2>

Set the logging level to **error**.

~~~
/usr/local/bin/distelli agent loglevel error
~~~

## <h3><a name="agent-run"></a>/usr/local/bin/distelli agent run</h3>

This is an internal command used to run the agent.

> **Caution:** This command is typically used only under the guidance of Puppet Pipelines support.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent run
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

This command is used by internal mechanisms to run the agent.

<h2>EXAMPLES</h2>

None.

## <h3><a name="agent-start"></a>/usr/local/bin/distelli agent start</h3>

This will start the agent. if the agent is already running, this will restart the agent.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent start
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

Used to start the agent. If the agent was installed with the `-nostart` option, this command `/usr/local/bin/distelli agent start` will start the agent.

<h2>EXAMPLES</h2>

Starting the agent.

~~~
/usr/local/bin/distelli agent start
Running under 'jdoe' account
Starting upstart daemon with name:\tdtk-supervise-cc123345677ad94a8d34ac610381242f9ae28bb8
~~~

## <h3><a name="agent-status"></a>/usr/local/bin/distelli agent status</h3>

Shows the current status of the agent.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent status
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

Use this command to check the status of the agent. This is useful when confirming that the agent was properly installed.

<h2>EXAMPLES</h2>

Look at the status of a running agent.

~~~
/usr/local/bin/distelli agent status
Distelli Agent (serverA) is Running with id 766b88c8-e925-11e4-ae8b-080027cc07f7
~~~

Look at the status of a stopped agent.

~~~
/usr/local/bin/distelli agent status
Distelli Agent is Stopped
~~~

## <h3><a name="agent-stop"></a>/usr/local/bin/distelli agent stop</h3>

Stops the running agent.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent stop
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

Use this to stop the agent running in the background.

<h2>EXAMPLES</h2>

Stop the agent.

~~~
/usr/local/bin/distelli agent stop
~~~

## <h3><a name="agent-uninstall"></a>/usr/local/bin/distelli agent uninstall</h3>

Use this to uninstall the agent.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent uninstall
~~~

<h2>OPTIONS</h2>

~~~
--yes
~~~

The `--yes` option facilitates a quiet deletion and auto-answers `yes` to the **Continue? (yes/no)** prompt.

<h2>USAGE</h2>

Uninstalling the agent will cause the agent to stop running and for the agent to destroy its Unique ID (UID).
<ul>
<li>All Pipelines deployed applications will be removed from the server.</li>

<li>The server will be removed from all environments.</li>

<li>The server will be removed from its Pipelines account.</li>

<li>The agent supervise process will no longer start at boot.</li>

</ul>

Uninstalling the agent doesn't remove the agent files, which allows for a future [/usr/local/bin/distelli agent install](./agent.html).

<h2>EXAMPLES</h2>


~~~
/usr/local/bin/distelli agent uninstall
Are you sure you want to uninstall the Distelli Agent? (to avoid this prompt, pass --yes flag)
 * All applications will be removed from this server
 * The server will be removed from all environments
 * The server will be removed from the web interface
 * The supervise process will be removed from 'upstart'
Continue? (yes/no)
yes
#
~~~

## <h3><a name="agent-version"></a>/usr/local/bin/distelli agent version</h3>

Shows the current version of the installed agent.

<h2>SYNTAX</h2>

~~~
/usr/local/bin/distelli agent version
~~~

<h2>OPTIONS</h2>

None.

<h2>USAGE</h2>

Show the version of the Pipelines agent.

<h2>EXAMPLES</h2>

~~~
/usr/local/bin/distelli agent version
Distelli Agent 3.34
Copyright (C) 2015 Distelli Inc.
~~~


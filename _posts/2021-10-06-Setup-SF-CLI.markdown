---
layout: post
title: Setup Salesforce CLI
date: 2021-10-6 
description: How to setup Salesforce CLI and Authorize your Salesforce Org. # Add post description (optional)
icon: install-cli-page.png
img: install-cli-page.png # Add image post (optional)
fig-caption: # Add figcaption (optional)
tags: [Salesforce, CLI, VScode]
---

## What we are about to learn
* Learn what is Salesforce CLI.
* How to Install Salesforce CLI.
* Authorize a Salesforce Org using SF CLI commands.

## Salesforce command line tool
Salesforce CLI is a tool provided by Salesforce which can be used to perform Salesforce actions right from your terminal program. SF CLI can be utilised by other softwares as well which are installed in your system for example VS Code, Node.js Applications etc.

You can use Salesforce CLI for:

* Aggregate all the tools you need to develop with and perform commands against your Salesforce org
* Synchronize source to and from scratch orgs.
* Create and manage orgs
* Import and Export Data
* Create and execute tests
* Create and Install Packages

And uses can be increased according to requirements, those were just few examples showing in what purpose Salesforce CLI can perform.

## Install Salesforce CLI on Windows
To install Salesforce command line tool you just need to follow below steps:

* You can download Salesforce CLI from [here](https://developer.salesforce.com/tools/sfdxcli). Choose your platform and install it on your device.

![Install CLI page]({{site.baseurl}}/assets/img/install-cli-page.png)

* After you have downloaded the file double click it and follow the steps to install it.                   

* During the installation it will ask you for the components to install make sure to select both 'Salesforce CLI version no.' and 'Set path to Salesforce CLI' and click next.

* Use the default installation options and keep pressing next.

* That's it CLI is installed on your device.

You can follow steps for Linux and Mac on this ![documentation](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_install_cli.htm).


## Test Command Line Interface

To check if CLI is installed on your device properly, open terminal ( In Windows press WIN+R and then type 'cmd' without quotes and press enter  AND In Mac just press Control + Option + Shift + T).

Now we will log into an organisation using the terminal commands. For this copy and paste this command in your terminal.

* sfdx force:auth:web:login ( To log into developer edition org or Production )
* sfdx force:auth:web:login --instanceurl "https://test.salesforce.com" ( To log into Sandbox )
* sfdx force:auth:web:login --instanceurl "https://customUrl" ( To log in with Custom url )

![Install CLI page]({{site.baseurl}}/assets/img/RunCommand-cli.png)

After pasting this command press enter and wait for a second. After a few seconds you'll see that your browser is opened with the Salesforce login tab. Type your credentials here and click on login button.

When your org is fully opened go back to the terminal, there you can see that a message showing that the org is authorize. 

![Install CLI page]({{site.baseurl}}/assets/img/success-cli.png)

So now its for sure that you have installed and setup the Salesforce command line interface successfully. Now to learn how to use other commands and perform actions on your org read my other blogs.

Thanks for Reading !!
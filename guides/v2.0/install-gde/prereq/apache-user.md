---
layout: default
group: install_pre
subgroup: Prerequisites
title: Create the Magento file system owner
menu_title: Create the Magento file system owner
menu_node:
menu_order: 02
github_link: install-gde/prereq/apache-user.md
---

#### Contents
*	<a href="#install-update-depend-user-over">Overview of ownership and permissions</a>
*	<a href="#install-update-depend-user-create">Create a user and give the user a strong password</a>
*	<a href="#install-update-depend-user-group">Options for shared groups</a>
*	<a href="#install-update-depend-user-switch">Switch to the Magento file system owner</a>

<div class="bs-callout bs-callout-tip">
  <p>Totally lost? Need a helping hand? Try our <a href="{{ site.gdeurl }}install-gde/install-quick-ref.html">installation quick reference (tutorial)</a> or <a href="{{ site.gdeurl }}install-gde/install-roadmap_part1.html">installation roadmap (reference)</a>.</p>
</div>

<h2 id="install-update-depend-user-over">Overview of ownership and permissions</h2>
Even in a development environment, you want your Magento installation to be secure. To help prevent issues related to unauthorized people or processes doing potentially harmful things to your system, we recommend some guidelines related to file system ownership and security:

*	The web server user should *not* own the files and directories on the Magento file system; however, the web server user must have write access to some directories.

	The *web server user* runs the web-based Setup Wizard installer and everything you do in the Magento Admin. This user must have the ability to write media files and so on. However, the user cannot *own* the files because that can potentially lead to security issues because any web-based process could potentially attack the Magento file system.

*	Another user should own the Magento files and directories; this user must not be `root`.

	This user runs the Magento cron job, command-line utilities, and has full control over all Magento files and directories. Because the user exists only on the server, it's very difficult for a malicious process to exploit it.

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>Although you can install and use the Magento software as the web server user, for the preceding reasons, we don't recommend it and don't discuss it in this guide.</p></span>
</div>

<h2 id="install-update-depend-user-create">Create a user and give the user a strong password</h2>
This section discusses how to create the Magento file system owner.

<div class="bs-callout bs-callout-warning">
    <p>If you don't have <code>root</code> privileges on your Magento server, you can use another local user account. Make sure the user has a strong password and continue with <a href="#install-update-depend-user-group">Put the Magento file system owner in the web server group</a>.</p>
</div>

To create a user on CentOS or Ubuntu, enter the following command as a user with `root` privileges:

	adduser <username>

To give the user a password, enter the following command as a user with `root` privileges:

	passwd <username>

Follow the prompts on your screen to create a password for the user.

For example, to create a user named `magento_user` and give the user a password, enter:

	sudo adduser magento_user
	sudo passwd magento_user

<div class="bs-callout bs-callout-warning">
    <p>Because the point of creating this user is to provide added security, make sure you create a <a href="https://en.wikipedia.org/wiki/Password_strength" target="_blank">strong password</a>.</p>
</div>

<h2 id="install-update-depend-user-group">Options for shared groups</h2>
To enable the web server to write files and directories in the Magento file system but to also maintain *ownership* by the Magento file system owner. This is necessary so both users can share access to Magento files. (This includes files created using the Magento Admin or other web-based utilities.)

You must share the users' groups in any of the following ways:

*	Put the Magento file system in the web server's group

	This method is simpler but otherwise equivalent to the other method.
*	Put each user in the other's group

See the following sections:

1.	<a href="#install-update-depend-user-findgroup">Find the web server group</a>
2.	Any of the following:

	*	<a href="#install-update-depend-user-add2group">Add the Magento file system owner to the web server's primary group</a>
	*	<a href="#install-update-depend-user-share-groups">Put each user in the other's group</a>

<h3 id="install-update-depend-user-findgroup">Find the web server group</h3>
To find the web server user's group:

*	CentOS: `egrep -i '^user|^group' /etc/httpd/conf/httpd.conf`

	Typically, the user and group name are both `apache`
*	Ubuntu: `ps aux | grep apache` to find the apache user, then `groups <apache user>` to find the group

	Typically, the user name and the group name are both `www-data`

Continue with either:

*	<a href="#install-update-depend-user-add2group">Put the Magento file system owner in the web server's group</a>
*	<a href="#install-update-depend-user-share-groups">Put each user in the other's group</a>

<h3 id="install-update-depend-user-add2group">Put the Magento file system owner in the web server's group</h3>
To put the Magento file system owner in the web server's primary group (assuming the typical Apache group name for CentOS and Ubuntu), enter the following command as a user with `root` privileges:

*	CentOS: `usermod -g apache <username>`
*	Ubuntu: `usermod -g www-data <username>`

For example, to add the user `magento_user` to the `apache` primary group on CentOS:

	usermod -g apache magento_user

To confirm your Magento user is a member of the web server group, enter the following command:

	groups <user name>

A sample result follows:

	magento_user : apache

To complete the task, restart the web server:

*	Ubuntu: `service apache2 restart`
*	CentOS: `service httpd restart`

<h3 id="install-update-depend-user-share-groups">Put each user in the other's group</h3>
An alternative to setting up group membership is to put the web server user in the Magento file system owner's group and vice versa. To put each user in the other's group, as a user with `root` privileges, enter the following command for each of the two users:

	usermod -a -G <groupname> <username>

For example,

	usermod -a -G apache magento_user
	usermod -a -G magento_user apache

To confirm the users' group membership, enter the following command for each user:

	groups <username>

Example:

	groups apache
	apache : apache magento_user

	groups magento_user
	magento_user : magento_user apache

To complete the task, restart the web server:

*	Ubuntu: `service apache2 restart`
*	CentOS: `service httpd restart`

<h2 id="install-update-depend-user-switch">Switch to the Magento file system owner</h2>
After you've performed the other tasks in this topic, enter one of the following commands to switch to that user:

*	Ubuntu: `su <username>`
*	CentOS: `su - <username>`

For example,

	su magento_user

### Next steps
*	<a href="{{ site.gdeurl }}install-gde/prereq/optional.html">Optional software</a>
*	<a href="{{ site.gdeurl }}install-gde/prereq/security.html">SELinux and iptables</a>
*	<a href="{{ site.gdeurl }}install-gde/install/pre-install.html">Your install or upgrade path</a>

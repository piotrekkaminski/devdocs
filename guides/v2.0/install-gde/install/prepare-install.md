---
layout: default
group: install_pre
subgroup: T_Developer
title: Update installation dependencies
menu_title: Update installation dependencies 
menu_node:
menu_order: 10
github_link: install-gde/install/prepare-install.md
redirect_from: /guides/v1.0/install-gde/install/prepare-install.html
---

#### Contents

*	<a href="#install-update-depend">Introduction to Magento installation dependencies</a>
*	<a href="#install-composer-install">Run `composer install` to update dependencies</a>
*	<a href="#instgde-prereq-compose-access">Set file system ownership and permissions</a>

  
<h2 id="install-update-depend">Introduction to Magento installation dependencies</h2>
We now use <a href="http://getcomposer.org">Composer</a> to resolve dependencies before you install the Magento software and extensions.

Composer is a separate application that manages PHP dependencies. Before you can install the Magento software, you must perform the following tasks in the order shown:

1.	<a href="{{ site.gdeurl }}install-gde/prereq/dev_install.html">Install the Composer software</a>.
2.	<a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html">Create the Magento file system owner</a> so Composer writes files to the web server docroot as the correct user.
2.	Run the <a href="#install-composer-install"><code>composer install</code> command</a> from your Magento root directory (for example, `/var/www/magento2/`).

	The Magento root directory is a subdirectory of your web server's docroot. Need help locating the docroot? Click <a href="{{ site.gdeurl }}install-gde/basics/basics_docroot.html">here</a>.

	<div class="bs-callout bs-callout-info" id="info">
  		<p>If the following error displays, see <a href="{{ site.gdeurl }}install-gde/trouble/tshoot_composer-fail.html">troubleshooting</a>:</p>
  		<pre>file_get_contents(app/etc/NonComposerComponentRegistration.php): failed to open stream: No such file or directory</pre>
	</div>

For you to be able to run the Magento application, make sure you perform all tasks as a user with privileges to write to the web server docroot. One way to do this is to log in as or switch to the <a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html#install-update-depend-user-switch">switch to the Magento file system owner</a>.

<h2 id="install-composer-install">Run <code>composer install</code> to update dependencies</h2>
Update installation dependencies as follows:

1.	Log in to your Magento server as the Magento file system owner or <a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html">switch to that user</a>.
2.	Change to the Magento installation directory and run `composer install`. Examples:

	CentOS:

		cd /var/www/html/magento2 && composer install

	Ubuntu:

		cd /var/www/magento2 && composer install

	This command updates package dependencies and can take a few minutes to complete.

	The following error might display:

		[Composer\Downloader\TransportException]
			The "https://repo.magento.com/archives/magento/composer/magento-composer-1.0.2.0.zip" file could not be downloaded (HTTP/1.1 404 Not Found)

	If so, create <a href="{{ site.gdeurl }}install-gde/prereq/dev_install.html#instgde-prereq-compose-clone-auth">`auth.json`</a> in the Magento file system owner's `<home>/.composer` directory and run `composer install` again.

<h2 id="instgde-prereq-compose-access">Set file system ownership and permissions</h2>
The following sections discuss how to set file system ownership and permissions:

*	<a href="#install-perms-import">Why we recommend you set file system permissions</a>
*	<a href="#install-perms-set">File system permissions and ownership</a>

<h3 id="install-perms-import">Why we recommend you set file system permissions</h3>
{% include install/file-system-perms1-why.html %}

<h3 id="install-perms-set">File system permissions and ownership</h3>
{% include install/file-system-perms2-how.md %}

#### Next step
Install the Magento software:

*	<a href="{{ site.gdeurl }}install-gde/install/cli/install-cli.html">Command line</a>
*	<a href="{{ site.gdeurl }}install-gde/install/web/install-web.html">Setup Wizard</a>
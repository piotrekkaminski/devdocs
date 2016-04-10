---
layout: default
group: compman
subgroup: ZZ_Troubleshooting
title: "We're sorry, we can't take that action right now"
menu_title: "We're sorry, we can't take that action right now"
menu_node: 
menu_order: 2
github_link: comp-mgr/trouble/cman/were-sorry.md
---

<h2 id="trouble-update-were-sorry">"We're sorry, we can't take that action right now"</h2>
The following error might display at the start of your upgrade:

<img src="{{ site.baseurl }}common/images/upgr-sorry.png" width="600px">

See one of the following sections for possible solutions:

*	[Problem: you're not authenticated](#not-auth)
*	[Problem: the updater application isn't initialized](#updater)
*	[Problem: missing `.gitignore` files](#missing-ignore)

### Problem: you're not authenticated {#not-auth}
You might not have entered your authentication keys in the Magento Admin.

#### Solution
Enter your <a href="{{ site.gdeurl }}comp-mgr/prereq/prereq_auth-token.html">authentication keys</a> in the Admin. Try your upgrade again.

If that doesn't work, try generating <a href="{{ site.gdeurl }}install-gde/prereq/connect-auth.html">new authentication keys</a> and enter those in the Admin. Then try your upgrade again.

### Problem: the updater application isn't initialized {#updater}
In some cases (especially if you downloaded the Magento software from <a href="https://packagist.org/" target="_blank">packagist</a>), the updater application might not be initialized. (A common way for this to happen is to not specify our `https://repo.magento.com` repository in the `composer create-project` command.)

The updater application uses a cron job to run the upgrade; if it's not initialized, your update fails.

#### Solution
Modify Magento's `composer.json` to reference the `https://repo.magento.com` repository and run `composer install` in the updater's root directory to resolve dependencies and initialize it as follows:

1.	Log in to your Magento server as the <a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html">Magento file system owner</a>.
2.	Change to your Magento installation directory.
3.	Back up your existing `composer.json`:

		cp composer.json composer.json.bak

4.	Open `composer.json` in a text editor.
5.	To the `repositories` section, add the following:

			{
				"type": "composer",
				"url": "https://repo.magento.com/"
			}

    Example:

		"repositories": [
				{
					"type": "composer",
					"url": "https://repo.magento.com/"
				}
			]

6.	Save your changes to `composer.json` and exit the text editor.
7.	Change to the `update` subdirectory, where the updater is located.
8.	Enter the following command:

		composer install
9.	After the command completes, try the upgrade again.

### Problem: missing `.gitignore` files {#missing-ignore}
If you downloaded a compressed archive, there might have been missing `.gitignore` files that prevent the upgrade from completing properly. To apply our update, patch `magento/magento-composer-installer` then run `composer update` from your Magento installation directory. 

#### Solution
To solve this issue:

1.	Log in to your Magento server as the <a href="{{ site.gdeurl }}install-gde/prereq/apache-user.html">Magento file system owner</a>.
2.	Change to your Magento installation directory.
3.	Run the following commands in the order shown:

		composer update magento/magento-composer-installer
		composer update

4.	Try your upgrade again.
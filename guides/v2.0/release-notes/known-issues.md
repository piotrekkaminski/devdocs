---
layout: default
group: 
title: Release Notes
menu_title: Known issues
menu_node: 
menu_order: 2
github_link: release-notes/known-issues.md
redirect_from: /guides/v1.0/release-notes/known-issues.html
---

<h2 id="known-devbeta">Known issues</h2>
This page discusses known issues in all Magento 2 releases starting with Developer Beta in December, 2014.

We have identified the following known issues in this release:

<!-- *   <a href="#known-devbeta-sampledata">Magento sample data is available only if you edit composer.json</a>
 -->
*   <a href="known-composer-clear-cache">You might need to clear your Composer cache</a>
*   <a href="#known-devrc-php">Known issue with timezone in certain PHP versions</a>
*   <a href="#known-devbeta-xdebug">Known issue with xdebug</a>
*   <a href="#known-devbeta-storefront-err">Access errors</a>
*   <a href="#known-devbeta-wiz-fail-bogus">Setup Wizard reports failure falsely</a>
*   <a href="#known-devbeta-wiz-fail-installog">Setup Wizard fails because of no installation log</a>
<!-- *   <a href="#known-devbeta-wiz-fail-session-save">session.save_path issue</a> -->

<!-- <h3 id="known-issue-sample">Issue installing optional sample data</h3> -->
<!-- https://jira.corp.x.com/browse/MAGETWO-32879 -->
<!-- Errors display when you attempt to install optional Magento sample data. We are working on this issue and expect a resolution in the near future. -->

<h3 id="known-composer-clear-cache">You might need to clear your Composer cache</h3>
{% include install/composer-clear-cache.html %}

<h3 id="known-devrc-php">Known issue with timezone in certain PHP versions</h3>
This issue affects builds *earlier than* 0.74-beta10 only. If you have a later build, you can ignore this issue.

There is a <a href="https://bugs.php.net/bug.php?id=66985" target="_blank">known PHP issue</a> with versions:

*   5.5.10&ndash;5.5.16
*   5.6.0

This issue prevents users from being able to set their timezones to Greenwich time and several other time zones. 

To work around this issue, after installing the Magento 2 software, edit the following files:

*   `app/code/Magento/Config/Model/Config/Backend/Locale/Timezone.php`
*   `lib/internal/Magento/Framework/Locale/Lists.php`
*   `setup/src/Magento/Setup/Model/Lists.php`

In each file, change the value of `$zones` as follows:

from

    $zones = \DateTimeZone::listIdentifiers(\DateTimeZone::ALL_WITH_BC);

to

    $zones = \DateTimeZone::listIdentifiers(\DateTimeZone::ALL);


<h3 id="known-devbeta-xdebug">Known issue with xdebug</h3>
If you use the optional PHP extension `xdebug`, you can encounter exceptions:

*   During installation 
*   Accessing either the Magento Admin or storefront after a successful installation 

Sample exception:

    Fatal error: Maximum function nesting level of '100' reached, aborting!

To resolve this issue, you can:

*   Disable the `xdebug` extension.
*   Set the value of `xdebug.max_nesting_level` to a value of 200 or more. For more information, see <a href="http://xdebug.org/docs/basic#max_nesting_level" target="_blank">xdebug documentation</a>.

After you change the configuration of or disable `xdebug`, restart Apache:

*   CentOS: `sudo service httpd restart`
*   Ubuntu: `sudo service apache2 restart`

<h3 id="known-devbeta-storefront-err">Access errors</h3>

<!-- <a href="https://jira.corp.x.com/browse/MAGETWO-31834">MAGETWO-31834</a> and <a href="https://jira.corp.x.com/browse/MAGETWO-31180">MAGETWO-31180</a> --> Errors might display when you attempt to access the Magento storefront or Magento Admin after installation:

Storefront:

    "Can't create directory /var/www/html/m/var/generation/Magento/Framework/App/PageCache/Identifier/."
    #0 /var/www/html/m/lib/internal/Magento/Framework/Code/Generator/Autoloader.php(34): Magento\Framework\Code\Generator->generateClass('Magento\\Framewo...')
    #1 [internal function]: Magento\Framework\Code\Generator\Autoloader->load('Magento\\Framewo...')
    #2 [internal function]: spl_autoload_call('Magento\\Framewo...')
    ... more

Magento Admin:

    "Class Magento\Logging\Model\FlagFactory does not exist"
    "#0 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/Definition/Runtime.php(46): Magento\Framework\Code\Reader\ClassReader->getConstructor('Magento\\Logging...')
    #1 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/Factory/Factory.php(170): Magento\Framework\ObjectManager\Definition\Runtime->getParameters('Magento\\Logging...')
    #2 /var/www/html/ui/lib/internal/Magento/Framework/ObjectManager/ObjectManager.php(71): Magento\Framework\ObjectManager\Factory\Factory->create('Magento\\Logging...')
    ... more

In either case, try accessing the storefront or Magento Admin again.

<h3 id="known-devbeta-wiz-fail-bogus">Setup Wizard reports failure falsely</h3>

<!-- <a href="https://jira.corp.x.com/browse/MAGETWO-31949">MAGETWO-31949</a> --> In some cases, the Setup Wizard appears to have failed when it has not failed. 

Symptoms:

*   The following message displays at the top of your browser on the last page: `Installation is incomplete. Check the console log for errors before trying again.`
*   If you open the console, a success message displays at the bottom with no errors or exceptions.

In this case, the installation *was* successful. You can access the storefront and Magento Admin as discussed in <a href="{{ site.gdeurl }}install-gde/install/verify.html">Verify the installation</a>.

To access your Magento-created encryption key:

1.  Log in to your Magento server as a user with `root` privileges.
2.  Do any of the following:

    *   Build 0.74-beta9 or earlier: Open `<your Magento install dir>/app/etc/config.php` in a text editor.
    *   Build 0.74-beta10 or later: Open `<your Magento install dir>/app/etc/env.php` in a text editor.
    
3.  Locate the value of `'key' =>`.
        
This is your encryption key.

<h3 id="known-devbeta-wiz-fail-installog">Setup Wizard fails because of no installation log</h3>

<!-- <a href="https://jira.corp.x.com/browse/MAGETWO-31850">MAGETWO-31850</a> -->In some cases (such as running the Setup Wizard in two browser windows or tab pages at the same time), the installation fails because it cannot create `install.log`. 

To work around this issue, see <a href="{{ site.gdeurl }}install-gde/trouble/tshoot_install-log.html">Installation fails; cannot create install.log</a>

<!-- <h3 id="known-devbeta-wiz-fail-session-save">session.save_path issue</h3>

<!-- <a href="https://jira.corp.x.com/browse/MAGETWO-31851">MAGETWO-31851</a> and <a href="https://github.com/magento/magento2/issues/792">GitHub issue 792</a> --><!-- There is a known issue that prevents the usage of <a href="http://php.net/manual/en/configuration.changes.php" target="_blank">php_admin_value</a> for some session configuration settings. Specifically, we are aware that the <a href="http://php.net/manual/en/session.configuration.php#ini.session.save-path" target="_blank">session.save_path</a> cannot be set with `php_admin_value` at this time.

Workarounds:

*   If you're using a hosting provider that does not allow you to change the value of `php_admin_value`, there is no workaround currently. However, the only known instance that we are aware of at this time is ISPManager/ISPConfig which appears to have a <a href="http://www.howtoforge.com/forums/showthread.php?t=61127" target="_blank">method of disabling</a> the `php_admin_value` setting.


*   If you're running the Magento software on your own server and you can log in as a user with `root` privileges, you can replace the `session.save_path` setting with a dependency injection call as follows:

1.  Log in to your Magento server as a user with `root` privileges.
2.  Open `php.ini` in a text editor.
3.  Search for `session.save_path`.
4.  Comment it out.
5.  Save your changes to `php.ini` and exit the text editor.
6.  Restart your web server.
7.  Open `<your Magento install dir>/app/etc/config.php` in a text editor.
8.  Add the following:

        ‘session’ => [
            ‘save_path’ => ‘<your session save path>'

1.  Save your changes and exit the text editor.
2.  Restart Apache.

    Ubuntu: `sudo service apache2 restart`
    CentOS: `sudo service httpd restart`

The Magento system now uses dependency injection for session save settings.

<h4>Finding php.ini</h4>

If you don't know where `php.ini` is located, use the following steps:

1.  If you haven't already done so, create <a href="{{ site.gdeurl }}install-gde/prereq/optional.html#install-optional-phpinfo">phpinfo.php</a>.
2.  Enter the following URL in your browser's address or location field:

    <code>http://&lt;your web server IP or host name>/&lt;path to docroot>/phpinfo.php</code>

3.  Look for the location of `php.ini`.

    `php.ini` is typically specified as **Loaded Configuration File** in the displayed results.

4.  As a user with <code>root</code> privileges, open `php.ini` in a text editor.
5.  Locate the value of `open_basedir` and change it.
6.  Save your changes to `php.ini`.
7.  Restart the web server. -->

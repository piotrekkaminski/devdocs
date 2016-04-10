---
layout: default
group: install_trouble
subgroup: PHP issues
title: During installation, PHP date warning
menu_title: During installation, PHP date warning
menu_node: 
menu_order: 20
github_link: install-gde/trouble/php/tshoot_php-date.md
redirect_from:
  -  /guides/v1.0/install-gde/trouble/tshoot_php-date.html
  -  /guides/v2.0/install-gde/trouble/tshoot_php-date.html
---

<h2 id="install-trouble-php-date">During installation, PHP date warning</h2>

### Details

During the installation, the following message displays: 

	PHP Warning:  date(): It is not safe to rely on the system's timezone settings. [more]

### Solution

Set the PHP timezone properly (<a href="{{ site.gdeurl }}install-gde/prereq/php-centos.html#instgde-prereq-timezone">CentOS</a>, <a href="{{ site.gdeurl }}install-gde/prereq/php-ubuntu.html#instgde-prereq-timezone">Ubuntu</a>).


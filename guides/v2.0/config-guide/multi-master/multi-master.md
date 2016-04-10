---
layout: default
group: config-guide
subgroup: Z_cqrs
title: Split database performance solution (Enterprise Edition only)
menu_title: Split database performance solution (Enterprise Edition only)
menu_order: 1
menu_node: parent
github_link: config-guide/multi-master/multi-master.md
---

<img src="{{ site.baseurl }}common/images/ee-only_large.png">

#### Contents
*	<a href="#config-ee-multidb-over">Overview of the split database solution</a>
*	<a href="#config-ee-multidb-prereq">Prerequisites</a>
*	<a href="{{ site.gdeurl }}config-guide/multi-master/multi-master_masterdb.html">Set up master databases</a>
*	<a href="{{ site.gdeurl }}config-guide/multi-master/multi-master_verify.html">Verify split databases</a>
*	<a href="{{ site.gdeurl }}config-guide/multi-master/multi-master_slavedb.html">Set up optional database replication</a>

<h2 id="config-ee-multidb-over">Overview of the split database solution</h2>
*This feature is available in Magento Enterprise Edition (EE) only.*

Magento 2 EE offers number of scalability advantages, including the ability to use three separate master databases for different functional areas of the Magento application.

Checkout, orders, and product data can all each use a separate master databases that you can optionally replicate. This separation independently scales load from website checkouts, order management activities, website browsing, and merchandising activities, depending on your needs.  These changes provide considerable flexibility in how the database tier can be scaled.

The `ResourceConnections` class provides the unified MySQL database connection to the Magento application. For queries to the master databases, we implement the <a href="https://en.wikipedia.org/wiki/Command%E2%80%93query_separation" target="_blank">Command Query Responsibility Segregation (CQRS)</a> database pattern. This pattern handles the logic for routing the read and write queries to the appropriate databases. Developers do not need to know which configuration is being used and there are no separate read and write database connections.

If you set up optional database replication, you get the following advantages:

*	Data backup
*	Data analysis without affecting the master database
*	Scalability

MySQL databases replicate asynchronously, which means slaves do not need to be connected permanently to receive updates from the master.

The following figure shows how this feature works.

<img src="{{ site.baseurl }}common/images/ee_split-db-diagram.png" alt="Magento EE uses different databases to store tables">

In Magento Community Edition (CE), only one master database is used.

Magento EE uses three master databases and a configurable number of slave databases for replication. Magento EE has a single interface for database connections, resulting in faster performance and better scalability.

<h2 id="config-ee-multidb-prereq">Prerequisites</h2>
The split database requires you to set up three MySQL master databases on any host (all three on the Magento server, each database on a separate server, and so on). These are the *master* databases and they're used as follows:

*	One master database for checkout tables
*	One master database for order management system (OMS) tables
*	One master database for the remainder of the Magento 2 application tables

In addition, you can optionally set up any number of *slave* databases that serve as load balancers and backups.

This guide discusses how to set up the master databases only. We provide sample configurations and references for you to set up slave databases if you wish.

In this guide, the three master databases are named:

*	`magento_checkout`
*	`magento_oms`
*	`magento`

(You can name your databases anything you wish.)

#### Next step
<a href="{{ site.gdeurl }}config-guide/multi-master/multi-master_masterdb.html">Set up master databases</a>
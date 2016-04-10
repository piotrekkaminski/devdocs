---
layout: default
group: config-guide
subgroup: Caching
title: Low-level cache options
menu_title: Low-level cache options
menu_order: 5
menu_node: 
github_link: config-guide/config/caching_low-level.md
---

The Magento application uses a low-level cache frontend and backend to provide access to the cache storage.

<h2 id="cache-lowlevel-front">Low-level frontend cache</h2>
Magento extends <a href="http://framework.zend.com/manual/1.12/en/zend.cache.frontends.html" target="_blank">Zend_Cache_Core</a> by implementing <a href="{{ site.mage2000url }}lib/internal/Magento/Framework/Cache/Core.php" target="_blank">Magento\Framework\Cache\Core</a> frontend cache. 

<h2 id="cache-lowlevel-front">Low-level backend cache</h2>
In general, the Magento application works with any backend cache that <a href="http://framework.zend.com/manual/1.12/en/zend.cache.backends.html" target="_blank">Zend_Cache Backends</a> supports. However, this guide covers only the following low-level backend caches:

*   <a href="{{ site.gdeurl }}config-guide/redis/config-redis.html">Redis</a>
*   <a href="{{ site.gdeurl }}config-guide/database/database.html">Database</a>
*   File system (default): No configuration is necessary to use file system caching.

<a href="{{ site.gdeurl }}config-guide/varnish/config-varnish.html">Varnish</a> doesn't require setting up a low-level cache backend.

<div class="bs-callout bs-callout-info" id="info">
  <p>We'll periodically add more low-level cache types so watch this space.</p>
</div> 

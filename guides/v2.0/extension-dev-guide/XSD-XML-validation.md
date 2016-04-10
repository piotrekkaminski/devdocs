---
layout: default
group: extension-dev-guide
subgroup: 3_Build
title: URN schema validation
menu_title: URN schema validation
menu_order: 6
github_link: extension-dev-guide/XSD-XML-validation.md

---
##{{page.menu_title}}


Each Magento module can contain XSD files for XML validation.

Magento uses [Uniform Resource Names](https://en.wikipedia.org/wiki/Uniform_Resource_Name) (URNs) to reference XML Schema declarations.

Magento supported URNs begin with `urn:magento`. Magento supports two XSD reference types:

* Module XSD
* Framework XSD


###Module XSD 

The syntax for the module XSD is a colon separated declaration. An example follows:

`urn:magento:module:Magento_Flow:flows/content.xsd`

where 

*  `urn:magento` is the URN identifier
*  `module` is the reference type identifier
*  `Magento_Flow` is the name of the module. This must be exactly the same as the module specified by ComponentRegistrar in the [registration.php](component-registration.html) file.
* `flows/content.xsd` is the relative path to the module&#8217;s directory.



###Framework XSD

The syntax for the framework XSD is a colon separated declaration. An example follows:

`urn:magento:framework:Api/etc/extension_attributes.xsd
where 

*  `urn:magento` is the URN identifier
*  `framework` is the reference type identifier. You can also add additional framework libraries as separate components with `framework-<sub-name>`
* `Api/etc/extension_attributes.xsd` is the relative path to the framework&#8217;s directory.


###Referencing a XSD from another XSD
Use URN notation to reference schema from inside a XSD document:

{% highlight XML %}

<xs:redefine schemaLocation="urn:magento:framework:Config/etc/view.xsd">


{% endhighlight %}

The URN resolution is invoked automatically by the libxml engine. Register the URN resolver by using `libxml_set_external_entity_loader`:

{% highlight XML %}
libxml_set_external_entity_loader(['Magento\Framework\Config\Dom\UrnResolver', 'registerEntityLoader']);
{% endhighlight %}

<div class="bs-callout bs-callout-info" id="info">
<span class="glyphicon-class">
  <p>The relative path to other XSDs cannot be used from inside the XSD file, because the entity loader fails to resolve the relative path.</p></span>
</div>




##Next

[Module Load Order](module-load-order.html)







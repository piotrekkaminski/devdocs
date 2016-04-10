---
layout: default
group: fedg
subgroup: B_Layouts
title: Customizing layout illustration
menu_title: Customizing layout illustration
menu_order: 7
github_link: frontend-dev-guide/layouts/layout-practice.md
redirect_from: /guides/v1.0/frontend-dev-guide/layouts/layout-practice.html
---

<h2>What's in this topic</h2>
This article features a step-by-step illustration of how a real-life layout customization task is performed. Namely, it illustrates how to change the layout of customer account links in a Magento store page header.

<h2>Moving customer account links</h2>
In their Orange theme, OrangeCo wants to transform the header links block to a drop-down, the way it is done in the Magento Luma theme:

<div style="border: 1px solid #ABABAB">
<img src="{{ site.baseurl }}common/images/layout_transform.png">
</div>

To do this, they need to wrap the list of header links with a container and add a greeting with a drop-down arrow before the list.

By default the rendered header links look like following:

<div style="border: 1px solid #ABABAB">
<img src="{{ site.baseurl }}common/images/layout_code_before1.png">
</div>

Needed:

<div style="border: 1px solid #ABABAB">
<img src="{{ site.baseurl }}common/images/layout_code_after.png">
</div>

<br>
<u>Step 1: Define the blocks</u>

OrangeCo <a href="{{site.gdeurl}}frontend-dev-guide/themes/theme-apply.html" target="_blank">applies the Luma theme</a>. Using the approach described in <a href="{{site.gdeurl}}frontend-dev-guide/themes/debug-theme.html" target="_blank">Locate templates, layouts, and styles</a> they find out that the blocks responsible for displaying the header links are defined in `<Magento_Customer_module_dir>/view/frontend/layout/default.xml`:

{%highlight xml%}
...
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceBlock name="top.links">
            <block class="Magento\Customer\Block\Account\Link" name="my-account-link">
                <arguments>
                    <argument name="label" xsi:type="string" translate="true">My Account</argument>
                </arguments>
            </block>
            <block class="Magento\Customer\Block\Account\RegisterLink" name="register-link">
                <arguments>
                    <argument name="label" xsi:type="string" translate="true">Register</argument>
                </arguments>
            </block>
            <block class="Magento\Customer\Block\Account\AuthorizationLink" name="authorization-link" template="account/link/authorization.phtml"/>
        </referenceBlock>
    </body>
</page>
{%endhighlight xml%}


<u>Step 2: Define the templates</u>

Similar to the way they defined the layout on the previous step, OrangeCo 
defines the template which is used for rearranging the links:

`<Magento_Customer_module_dir>/view/frontend/templates/account/customer.phtml`

{%highlight php%}
<?php if($this->customerLoggedIn()): ?>
    <li class="customer welcome customer-welcome">
        <span class="customer name" data-mage-init='{"dropdown":{}}' data-toggle="dropdown">
            <span><?php echo $this->getCustomerName(); ?></span>
            <button type="button" class="action switch"><span><?php echo __('Change')?></span></button>
        </span>
        <?php if($this->getChildHtml()):?>
        <div class="customer menu customer-menu" data-target="dropdown">
            <?php echo $this->getChildHtml();?>
        </div>
        <?php endif; ?>
    </li>
<?php endif; ?>
{%endhighlight php%}

<br>
<u>Step 3: Extend the base layout to add a block</u>

OrangeCo needs to create a new block, say, `header.links`, in the `header.panel` container, to move the links there. As the links can be added to this list by different modules, it is better to add this block to the `default.xml` page configuration of the `Magento_Theme` module.

So the following <a href="{{site.gdeurl}}frontend-dev-guide/layouts/layout-extend.html" target="_blank">extending</a> layout is added in the Orange theme:

    app/design/frontend/OrangeCo/orange/Magento_Theme/layout/default.xml

{%highlight xml%}
<page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
    <body>
        <referenceContainer name="header.panel">
            <block class="Magento\Framework\View\Element\Html\Links" name="header.links">
                <arguments>
                    <argument name="css_class" xsi:type="string">header links</argument>
                </arguments>
            </block>
        </referenceContainer>
    </body>
</page>
{%endhighlight xml%}

<br>

<u>Step 4: Move links</u>

To move the links to the `header.links` block, OrangeCo adds an extending layout:

`app/design/frontend/OrangeCo/orange/Magento_Customer/layout/default.xml`


{%highlight xml%}
    <page xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xsi:noNamespaceSchemaLocation="urn:magento:framework:View/Layout/etc/page_configuration.xsd">
        <body>
            <referenceBlock name="header.links">
                <block class="Magento\Customer\Block\Account\Customer" name="customer" template="account/customer.phtml" before="-"/>
                <block class="Magento\Customer\Block\Account\AuthorizationLink" name="authorization-link-login" template="account/link/authorization.phtml"/>
            </referenceBlock>
            <move element="register-link" destination="header.links"/>
            <move element="top.links" destination="customer"/>
            <move element="authorization-link" destination="top.links" after="-"/>
        </body>
    </page>
{%endhighlight xml%}

Now the customer links look like following:

<div style="border: 1px solid #ABABAB">
<img src="{{ site.baseurl }}common/images/layout_screen2.png">
</div>

The last touch is adding styles:

<div style="border: 1px solid #ABABAB">
<img src="{{ site.baseurl }}common/images/layout_screen3.png">
</div>





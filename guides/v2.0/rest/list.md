---
layout: default
group: rest
subgroup: A_rest
title: List of REST APIs by module
menu_title: List of REST APIs by module
menu_order: 3
github_link: rest/list.md
redirect_from: /guides/v1.0/rest/list.html
---

<h2 id="list">List of REST APIs</h2>

Updated October 2, 2015. Additions since the last update are marked with asterisks (*).

<h3>Backend</h3>

    GET    /V1/modules

<h3>Bundle</h3>

    POST   /V1/bundle-products/:sku/links/:optionId
    PUT    /V1/bundle-products/:sku/links/:id
    GET    /V1/bundle-products/:productSku/children
    DELETE /V1/bundle-products/:sku/options/:optionId/children/:childSku
    GET    /V1/bundle-products/:sku/options/all
    GET    /V1/bundle-products/options/types
    GET    /V1/bundle-products/:sku/options/:optionId
    POST   /V1/bundle-products/options/add
    PUT    /V1/bundle-products/options/:optionId
    DELETE /V1/bundle-products/:sku/options/:optionId

<h3>Catalog</h3>

    POST   /V1/products
    PUT    /V1/products/:sku
    DELETE /V1/products/:sku
    GET    /V1/products
    GET    /V1/products/:sku
    GET    /V1/products/attributes/types
    GET    /V1/products/attributes/:attributeCode
    GET    /V1/products/attributes
    GET    /V1/categories/attributes/:attributeCode
    GET    /V1/categories/attributes
    GET    /V1/categories/attributes/:attributeCode/options
    POST   /V1/products/attributes
    PUT    /V1/products/attributes/:attributeCode
    DELETE /V1/products/attributes/:attributeCode
    GET    /V1/products/types
    GET    /V1/products/attribute-sets/sets/list
    GET    /V1/products/attribute-sets/:attributeSetId
    DELETE /V1/products/attribute-sets/:attributeSetId
    POST   /V1/products/attribute-sets
    PUT    /V1/products/attribute-sets/:attributeSetId
    GET    /V1/products/attribute-sets/:attributeSetId/attributes
    POST   /V1/products/attribute-sets/attributes
    DELETE /V1/products/attribute-sets/:attributeSetId/attributes/:attributeCode
    GET    /V1/products/attribute-sets/groups/list
    POST   /V1/products/attribute-sets/groups
    PUT    /V1/products/attribute-sets/:attributeSetId/groups
    DELETE /V1/products/attribute-sets/groups/:groupId
    GET    /V1/products/attributes/:attributeCode/options
    POST   /V1/products/attributes/:attributeCode/options
    DELETE /V1/products/attributes/:attributeCode/options/:optionId
    GET    /V1/products/media/types/:attributeSetName
    * GET    /V1/products/:sku/media/:entryId
    POST   /V1/products/:sku/media
    PUT    /V1/products/:sku/media/:entryId
    DELETE /V1/products/:sku/media/:entryId
    GET    /V1/products/:sku/media
    GET    /V1/products/:sku/group-prices/:customerGroupId/tiers
    POST   /V1/products/:sku/group-prices/:customerGroupId/tiers/:qty/price/:price
    DELETE /V1/products/:sku/group-prices/:customerGroupId/tiers/:qty
    DELETE /V1/categories/:categoryId
    GET    /V1/categories/:categoryId
    POST   /V1/categories
    GET    /V1/categories
    PUT    /V1/categories/:id
    PUT    /V1/categories/:categoryId/move
    GET    /V1/products/options/types
    GET    /V1/products/:sku/options
    GET    /V1/products/:sku/options/:optionId
    POST   /V1/products/options
    PUT    /V1/products/options/:optionId
    DELETE /V1/products/:sku/options/:optionId
    GET    /V1/products/links/types
    GET    /V1/products/links/:type/attributes
    GET    /V1/products/:sku/links/:type
    POST   /V1/products/:sku/links
    DELETE /V1/products/:sku/links/:type/:linkedProductSku
    PUT    /V1/products/:sku/links
    GET    /V1/categories/:categoryId/products
    POST   /V1/categories/:categoryId/products
    PUT    /V1/categories/:categoryId/products
    DELETE /V1/categories/:categoryId/products/:sku

<h3>CatalogInventory</h3>

    GET    /V1/stockItems/:productSku
    * PUT    /V1/products/:productSku/stockItems/:itemId
    GET    /V1/stockItems/lowStock/
    GET    /V1/stockStatuses/:productSku

<h3>Checkout</h3>

    POST   /V1/carts/:cartId/shipping-information
    POST   /V1/carts/mine/shipping-information
    POST   /V1/carts/:cartId/totals-information
    POST   /V1/guest-carts/:cartId/totals-information
    POST   /V1/carts/mine/totals-information
    POST   /V1/guest-carts/:cartId/payment-information
    GET    /V1/guest-carts/:cartId/payment-information
    POST   /V1/carts/mine/payment-information
    GET    /V1/carts/mine/payment-information
    POST   /V1/guest-carts/:cartId/set-payment-information
    POST   /V1/carts/mine/set-payment-information

<h3>CheckoutAgreements</h3>

    GET    /V1/carts/licence

<h3>Cms</h3>

    GET    /V1/cmsPage/:pageId
    GET    /V1/cmsPage/search
    POST   /V1/cmsPage
    PUT    /V1/cmsPage/:id
    DELETE /V1/cmsPage/:pageId
    GET    /V1/cmsBlock/:blockId
    GET    /V1/cmsBlock/search
    POST   /V1/cmsBlock
    PUT    /V1/cmsBlock/:id
    DELETE /V1/cmsBlock/:blockId

<h3>ConfigurableProduct</h3>

    GET    /V1/configurable-products/:sku/children
    DELETE /V1/configurable-products/:sku/children/:childSku
    PUT    /V1/configurable-products/variation
    POST   /V1/configurable-products/:sku/child
    GET    /V1/configurable-products/:sku/options/:id
    GET    /V1/configurable-products/:sku/options/all
    POST   /V1/configurable-products/:sku/options
    PUT    /V1/configurable-products/:sku/options/:id
    DELETE /V1/configurable-products/:sku/options/:id

<h3>Customer</h3>

    GET    /V1/customerGroups/:id
    GET    /V1/customerGroups/default/:storeId
    GET    /V1/customerGroups/default
    GET    /V1/customerGroups/:id/permissions
    GET    /V1/customerGroups/search
    POST   /V1/customerGroups
    PUT    /V1/customerGroups/:id
    DELETE /V1/customerGroups/:id
    GET    /V1/attributeMetadata/customer/attribute/:attributeCode
    GET    /V1/attributeMetadata/customer/form/:formCode
    GET    /V1/attributeMetadata/customer
    GET    /V1/attributeMetadata/customer/custom
    GET    /V1/attributeMetadata/customerAddress/attribute/:attributeCode
    GET    /V1/attributeMetadata/customerAddress/form/:formCode
    GET    /V1/attributeMetadata/customerAddress
    GET    /V1/attributeMetadata/customerAddress/custom
    GET    /V1/customers/:customerId
    POST   /V1/customers
    PUT    /V1/customers/:id
    PUT    /V1/customers/me
    GET    /V1/customers/me
    PUT    /V1/customers/me/activate
    GET    /V1/customers/search
    PUT    /V1/customers/:email/activate
    PUT    /V1/customers/me/password
    GET    /V1/customers/:customerId/password/resetLinkToken/:resetPasswordLinkToken
    PUT    /V1/customers/password
    GET    /V1/customers/:customerId/confirm
    POST   /V1/customers/confirm
    PUT    /V1/customers/validate
    GET    /V1/customers/:customerId/permissions/readonly
    DELETE /V1/customers/:customerId
    POST   /V1/customers/isEmailAvailable
    GET    /V1/customers/addresses/:addressId
    GET    /V1/customers/me/billingAddress
    GET    /V1/customers/:customerId/billingAddress
    GET    /V1/customers/me/shippingAddress
    GET    /V1/customers/:customerId/shippingAddress
    DELETE /V1/addresses/:addressId

<h3>Directory</h3>

    * GET    /V1/directory/currency
    * GET    /V1/directory/countries
    * GET    /V1/directory/countries/:countryId

<h3>Downloadable</h3>

    GET    /V1/products/:sku/downloadable-links
    GET    /V1/products/:sku/downloadable-links/samples
    POST   /V1/products/:sku/downloadable-links
    PUT    /V1/products/:sku/downloadable-links/:id
    DELETE /V1/products/downloadable-links/:id
    POST   /V1/products/:sku/downloadable-links/samples
    PUT    /V1/products/:sku/downloadable-links/samples/:id
    DELETE /V1/products/downloadable-links/samples/:id

<h3>Eav</h3>

    GET    /V1/eav/attribute-sets/list
    GET    /V1/eav/attribute-sets/:attributeSetId
    DELETE /V1/eav/attribute-sets/:attributeSetId
    POST   /V1/eav/attribute-sets
    PUT    /V1/eav/attribute-sets/:attributeSetId

<h3>GiftMessage</h3>

    GET    /V1/carts/:cartId/gift-message
    GET    /V1/carts/:cartId/gift-message/:itemId
    POST   /V1/carts/:cartId/gift-message
    POST   /V1/carts/:cartId/gift-message/:itemId
    GET    /V1/carts/mine/gift-message
    GET    /V1/carts/mine/gift-message/:itemId
    POST   /V1/carts/mine/gift-message
    POST   /V1/carts/mine/gift-message/:itemId
    GET    /V1/guest-carts/:cartId/gift-message
    GET    /V1/guest-carts/:cartId/gift-message/:itemId
    POST   /V1/guest-carts/:cartId/gift-message
    POST   /V1/guest-carts/:cartId/gift-message/:itemId

<h3>Integration</h3>

    POST   /V1/integration/admin/token
    POST   /V1/integration/customer/token

<h3>Quote</h3>

    GET    /V1/carts/:cartId
    GET    /V1/carts
    POST   /V1/carts/
    POST   /V1/customers/:customerId/carts
    PUT    /V1/carts/:cartId
    POST   /V1/carts/mine
    GET    /V1/carts/mine
    PUT    /V1/carts/mine/order
    GET    /V1/guest-carts/:cartId
    POST   /V1/guest-carts
    PUT    /V1/guest-carts/:cartId
    PUT    /V1/guest-carts/:cartId/order
    PUT    /V1/carts/:cartId/selected-shipping-method
    GET    /V1/carts/:cartId/selected-shipping-method
    GET    /V1/carts/:cartId/shipping-methods
    PUT    /V1/carts/mine/selected-shipping-method
    GET    /V1/carts/mine/selected-shipping-method
    GET    /V1/carts/mine/shipping-methods
    POST   /V1/carts/mine/estimate-shipping-methods
    POST   /V1/carts/mine/estimate-shipping-methods-by-address-id
    PUT    /V1/guest-carts/:cartId/selected-shipping-method
    GET    /V1/guest-carts/:cartId/selected-shipping-method
    GET    /V1/guest-carts/:cartId/shipping-methods
    POST   /V1/guest-carts/:cartId/estimate-shipping-methods
    GET    /V1/carts/:cartId/items
    POST   /V1/carts/items
    PUT    /V1/carts/items/:itemId
    DELETE /V1/carts/:cartId/items/:itemId
    GET    /V1/guest-carts/:cartId/items
    POST   /V1/guest-carts/items
    PUT    /V1/guest-carts/items/:itemId
    DELETE /V1/guest-carts/:cartId/items/:itemId
    GET    /V1/carts/mine/items
    POST   /V1/carts/mine/items
    PUT    /V1/carts/mine/items/:itemId
    DELETE /V1/carts/mine/items/:itemId
    GET    /V1/carts/:cartId/selected-payment-method
    PUT    /V1/carts/:cartId/selected-payment-method
    GET    /V1/carts/:cartId/payment-methods
    GET    /V1/guest-carts/:cartId/selected-payment-method
    PUT    /V1/guest-carts/:cartId/selected-payment-method
    GET    /V1/guest-carts/:cartId/payment-methods
    GET    /V1/carts/mine/selected-payment-method
    PUT    /V1/carts/mine/selected-payment-method
    GET    /V1/carts/mine/payment-methods
    GET    /V1/carts/:cartId/billing-address
    POST   /V1/carts/:cartId/billing-address
    GET    /V1/guest-carts/:cartId/billing-address
    POST   /V1/guest-carts/:cartId/billing-address
    GET    /V1/carts/mine/billing-address
    POST   /V1/carts/mine/billing-address
    GET    /V1/carts/:cartId/coupons
    PUT    /V1/carts/:cartId/coupons/:couponCode
    DELETE /V1/carts/:cartId/coupons
    GET    /V1/guest-carts/:cartId/coupons
    PUT    /V1/guest-carts/:cartId/coupons/:couponCode
    DELETE /V1/guest-carts/:cartId/coupons
    GET    /V1/carts/mine/coupons
    PUT    /V1/carts/mine/coupons/:couponCode
    DELETE /V1/carts/mine/coupons
    GET    /V1/carts/:cartId/shipping-address
    POST   /V1/carts/:cartId/shipping-address
    GET    /V1/guest-carts/:cartId/shipping-address
    POST   /V1/guest-carts/:cartId/shipping-address
    GET    /V1/carts/mine/shipping-address
    POST   /V1/carts/mine/shipping-address
    PUT    /V1/carts/:cartId/order
    GET    /V1/carts/:cartId/totals
    PUT    /V1/guest-carts/:cartId/collect-totals
    GET    /V1/guest-carts/:cartId/totals
    GET    /V1/carts/mine/totals
    PUT    /V1/carts/mine/collect-totals

<h3>Sales</h3>

    GET    /V1/orders/:id
    GET    /V1/orders
    GET    /V1/orders/:id/statuses
    POST   /V1/orders/:id/cancel
    POST   /V1/orders/:id/emails
    POST   /V1/orders/:id/hold
    POST   /V1/orders/:id/unhold
    POST   /V1/orders/:id/comments
    GET    /V1/orders/:id/comments
    PUT    /V1/orders/create
    PUT    /V1/orders/:parent_id
    GET    /V1/invoices/:id
    GET    /V1/invoices
    GET    /V1/invoices/:id/comments
    POST   /V1/invoices/:id/emails
    POST   /V1/invoices/:id/void
    POST   /V1/invoices/:id/capture
    POST   /V1/invoices/comments
    POST   /V1/invoices/
    GET    /V1/creditmemo/:id/comments
    GET    /V1/creditmemos
    GET    /V1/creditmemo/:id
    PUT    /V1/creditmemo/:id
    POST   /V1/creditmemo/:id/emails
    POST   /V1/creditmemo/:id/comments
    POST   /V1/creditmemo
    GET    /V1/shipment/:id
    GET    /V1/shipments
    GET    /V1/shipment/:id/comments
    POST   /V1/shipment/:id/comments
    POST   /V1/shipment/:id/emails
    POST   /V1/shipment/track
    DELETE /V1/shipment/track/:id
    POST   /V1/shipment/
    GET    /V1/shipment/:id/label
    POST   /V1/orders/
    GET    /V1/transactions/:id
    GET    /V1/transactions

<h3>SalesRule</h3>

    * GET    /V1/salesRules/:ruleId
    * GET    /V1/salesRules/search
    * POST   /V1/salesRules
    * PUT    /V1/salesRules/:ruleId
    * DELETE /V1/salesRules/:ruleId
    * GET    /V1/coupons/:couponId
    * GET    /V1/coupons/search
    * POST   /V1/coupons
    * PUT    /V1/coupons/:couponId
    * DELETE /V1/coupons/:couponId
    * POST   /V1/coupons/generate
    * POST   /V1/coupons/deleteByIds
    * POST   /V1/coupons/deleteByCodes

<h3>Search</h3>

    GET    /V1/search

<h3>Store</h3>

    * GET    /V1/store/storeViews
    * GET    /V1/store/storeGroups
    * GET    /V1/store/websites
    * GET    /V1/store/storeConfigs

<h3>Tax</h3>

    POST   /V1/taxRates
    GET    /V1/taxRates/:rateId
    PUT    /V1/taxRates
    DELETE /V1/taxRates/:rateId
    GET    /V1/taxRates/search
    POST   /V1/taxRules
    PUT    /V1/taxRules
    DELETE /V1/taxRules/:ruleId
    GET    /V1/taxRules/:ruleId
    GET    /V1/taxRules/search
    POST   /V1/taxClasses
    GET    /V1/taxClasses/:taxClassId
    PUT    /V1/taxClasses/:classId
    DELETE /V1/taxClasses/:taxClassId
    GET    /V1/taxClasses/search


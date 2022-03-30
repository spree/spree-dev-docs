---
title: Products
section: internals
order: 2
---

# Products

## Overview

`Product` records track unique products within your store. These differ from [Variants](products.md#variants), which track the unique variations of a product. For instance, a product that's a T-shirt would have variants denoting its different colors. Together, Products and Variants describe what is for sale.

Products have the following attributes:

* `name`: short name for the product
* `description`: The most elegant, poetic turn of phrase for describing your product's benefits and features to your site visitors
* `slug`: An SEO slug based on the product name that is placed into the URL for the product
* `available_on`: The first date the product becomes available for sale online in your shop. If you don't set the `available_on` attribute, the product will not appear among your store's products for sale.
* `discontinue_on`: Date when the product will become unavailable for sale online in your shop
* `deleted_at`: The date the product is marked as deleted
* `meta_title`: Optional title used for search engines instead of `name`
* `meta_description`: A description targeted at search engines for search engine optimization \(SEO\)
* `meta_keywords`: Several words and short phrases separated by commas, also targeted at search engines

To understand how variants come to be, you must first understand option types and option values.

## Option Types and Option Values

Option types denote the different options for a variant. A typical option type would be a size, with that option type's values being something such as "Small", "Medium" and "Large". Another typical option type could be a color, such as "Red", "Green", or "Blue".

A product can be assigned many option types, but must be assigned at least one if you wish to create variants for that product.

## Variants

`Variant` records track the individual variants of a `Product`. Variants are of two types: master variants and normal variants.

Variant records can track some individual properties regarding a variant, such as height, width, depth, and cost price. These properties are unique to each variant, and so are different from [Product Properties](products.md#product-properties), which apply to all variants of that product.

### Master Variants

Every single product has a master variant, which tracks basic information such as a count on hand, a price and a SKU. Whenever a product is created, a master variant for that product will be created too.

Master variants are automatically created along with a product and exist for the sole purpose of having a consistent API when associating variants and [line items](orders.md#line-items). If there were no master variant, then line items would need to track a polymorphic association which would either be a product or a variant.

By having a master variant, the code within Spree to track is simplified.

### Normal Variants

Variants which are not the master variant are unique based on [option type and option value](products.md#option-types-and-option-values) combinations. For instance, you may be selling a product which is a Baseball Jersey, which comes in the sizes "Small", "Medium" and "Large", as well as in the colors of "Red", "Green" and "Blue". For this combination of sizes and colors, you would be able to create 9 unique variants:

* Small, Red
* Small, Green
* Small, Blue
* Medium, Red
* Medium, Green
* Medium, Blue
* Large, Red
* Large, Green
* Large, Blue

### Default Variant

To simplify things you can call `product.default_variant` to get the default Variant. If a product has multiple Variants it will return the first non-master Variant based on their sort position set in the Admin Panel. If there are no non-master Variants it will return the Master Variant.

## Images

Images link to a product through its master variant. The sub-variants for the product may also have their own unique images to differentiate them in the frontend.

Spree automatically handles the creation and storage of several size versions of each image \(via Active Storage\). See [Images Customization](../customization/images.md) section.

## Product Properties

Product properties track individual attributes for a product that don't apply to all products. These are typically additional information about the item. For instance, a T-Shirt may have properties representing information about the kind of material used, as well as the type of fit the shirt is.

A `Property` should not be confused with an [`OptionType`](products.md#option-types-and-option-values), which is used when defining [Variants](products.md#variants) for a product.

You can retrieve the value for a property on a `Product` object by calling the `property` method on it and passing through that property's name:

```bash
product.property("material")
=> "100% Cotton"
```

You can set a property on a product by calling the `set_property` method:

```ruby
product.set_property("material", "100% cotton")
```

If this property doesn't already exist, a new `Property` instance with this name will be created.

## Prices

`Price` objects track a price for a particular currency and variant combination. For instance, a [Variant](products.md#variants) may be available for $15 \(15 USD\) and €7 \(7 Euro\).

Spree behind the scenes uses [Ruby Money gem](https://github.com/RubyMoney/money) with some [additional](https://github.com/spree/spree/blob/master/core/app/models/concerns/spree/display_money.rb) [tweaks](https://github.com/spree/spree/blob/master/core/lib/spree/money.rb).

If a product doesn't have a price in the selected currency it won't show up in the Storefront API by default. 

To fetch a list of currencies that given product is available in, call `prices` to get a list of related `Price` objects:

```bash
product.prices
=> [#<Spree::Price id: 2 ...]
```

To find a list of currencies that Variant is available in, call `prices` to get a list of related `Price` objects:

```bash
product.default_variant.prices
=> [#<Spree::Price id: 2 ...]
```

To find Product price in a selected currency via [ISO symbol](https://www.iban.com/currency-codes):

```bash
product.price_in('EUR')
=> #<Spree::Price id: 232, variant_id: 232, amount: 0.8499e2, currency: "EUR", deleted_at: nil, created_at: "2021-08-16 19:41:55.888522000 +0000", updated_at: "2021-08-16 19:41:55.888522000 +0000", compare_at_amount: nil, preferences: nil>
```

If there's no price set for this currency this will return a `Price.new(currency: 'EUR')` object.

To find Variant's price in a selected currency:

```bash
product.default_variant.price_in('EUR')
=> #<Spree::Price id: 232, variant_id: 232, amount: 0.8499e2, currency: "EUR", deleted_at: nil, created_at: "2021-08-16 19:41:55.888522000 +0000", updated_at: "2021-08-16 19:41:55.888522000 +0000", compare_at_amount: nil, preferences: nil>
```

There are also other helpful methods available such as:

#### Getting amount \(number\)

```text
product.default_variant.amount_in('EUR')
 => 0.8499e2
```

#### Getting amount \(string\)

```text
product.default_variant.amount_in('EUR').to_s
 => "84.99"
```

## Prototypes

A prototype is a useful way to share common `OptionType` and `Property` combinations amongst many different products. For instance, if you're creating a lot of shirt products, you may wish to maintain the "Size" and "Color" option types, as well as a "Fitting Type" property.


## Digital Assets

Besides psychical goods Spree offers the ability to retail digital goods delivered via an Active Storage download link, download links can be limited with a download count and expire time through the store settings area.

Ideally each product should be either a psychical, or a digital product. If the product you are creating has no options (variants) this product becomes a digital product when a digital asset is attached.
If the product you are creating has several variants, each variant is treated as physical or digital on a per variant basis when the variant has a digital asset attached.

An example use case of a product with many digital variants would be if you want to give the customer the option to purchase an eBook in a specific language, each variant being a designated language and the appropriate eBook translation uploaded to each variant,
the customer viewing the eBook product can select the language of choice and the file they receive upon purchase will be the asset attached the variant the customer purchased.

#### Private Digital Asset Storage

When storing digital goods (assets) on your chosen storage provider you will want to host these on a separate bucket to the one you are using for the public product images, to set-up a private storage bucket for private files follow these steps:

1. Create a new private bucket on your asset hosting service provider.

2. Within the `config/storage.yml` file add the credentials of your new private bucket and give this configuration a name of your choosing, here we have used `spree_private:`.

```yml
---
amazon:
  service: S3
  access_key_id: <%= Rails.application.credentials.dig(:aws, :access_key_id) %>
  secret_access_key: <%= Rails.application.credentials.dig(:aws, :secret_access_key) %>
  region: us-east-1
  bucket: the_public_bucket

spree_private:
  service: S3
  access_key_id: <%= Rails.application.credentials.dig(:aws, :access_key_id) %>
  secret_access_key: <%= Rails.application.credentials.dig(:aws, :secret_access_key) %>
  region: us-east-1
  bucket: the_private_bucket
```

2. Within your Spree Rails app locate the spree.rb initializer file, and add the following line referencing the name of your private bucket service configuration.

```ruby
# initializers/spree.rb
Spree.private_storage_service_name = 'spree_private'
```

## Taxons and Taxonomies

Taxonomies provide a simple, yet robust way of categorizing products by enabling store administrators to define as many separate structures as needed.

When working with Taxonomies there are two key terms to understand:

* `Taxonomy` – a hierarchical list which is made up of individual Taxons. Each taxonomy relates to one `Taxon`, which is its root node.
* `Taxon` – a single child node which exists at a given point within a `Taxonomy`. Each `Taxon` can contain many \(or no\) sub / child taxons. Store administrators can define as many Taxonomies as required, and link a product to multiple Taxons from each Taxonomy.

By default, both Taxons and Taxonomies are ordered by their `position` attribute.

Taxons use the [Nested set model](http://en.wikipedia.org/wiki/Nested_set_model) for their hierarchy. The `lft` and `rgt` columns in the `spree_taxons` table represent the locations within the hierarchy of the item. This logic is handled by the [awesome nested set](https://github.com/collectiveidea/awesome_nested_set) gem.

Taxons link to products through an intermediary model called `Classification`. This model exists so that when a product is deleted, all of the links from that product to its taxons are deleted automatically. A similar action takes place when a taxon is deleted; all of the links to products are deleted automatically.

Linking to a taxon in a controller or a template should be done using the `spree.nested_taxons_path` helper, which will use the taxon's permalink to generate a URL such as `/t/categories/brand`.

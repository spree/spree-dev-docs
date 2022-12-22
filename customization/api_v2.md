---
title: API v2
section: customization
order: 6
description: >-
  This page covers adding new Storefront API endpoints and customization of
  existing ones
---

# Storefront API

## Customizing existing API endpoints

### Customizing JSON response

Spree uses [JSON API serializers](https://github.com/jsonapi-serializer/jsonapi-serializer) to represent data returned by API endpoints. 

You can easily swap OOTB Spree serializers with your own thanks to [Spree Dependencies](dependencies.md). 

#### Adding custom attributes

{% hint style="info" %}
Generally it's recommended to use [Properties](../internals/products.md#product-properties) and [OptionTypes/Option Values](../internals/products.md#option-types-and-option-values) for custom attributes and not to modify the Spree database schema
{% endhint %}

Let's say you want to customize the Storefront API's [Product serializer](https://github.com/spree/spree/blob/master/api/app/serializers/spree/v2/storefront/product_serializer.rb) to include you custom database column `my_newcustom_attribute` that you've added to the `spree_products` database table.

Let's start with creating a new serializer file in your project's `app/serializers` directory, that is `app/serializers/my_product_serializer.rb`:

```ruby
class MyProductSerializer < Spree::V2::Storefront::ProductSerializer
  attribute :my_new_custom_attribute
end
```

Now let's tell Spree to use this new serializer, in `config/initializers/spree.rb` please set:

```ruby
Spree::Api::Dependencies.storefront_product_serializer = 'MyProductSerializer'
```

Restart the webserver and hit the [Products API ](https://api.spreecommerce.org/docs/api-v2/b3A6MzE0Mjc2Mg-list-of-products)to notice that the payload now includes your new attribute. alongside the standard output.

#### Adding a new association

Let's say you've created a new model called `Video` that belongs to `Product` \(_Product has multiple Videos_\).

Let's create a new serializer `app/serializers/video_serializer.rb`:

```ruby
class VideoSerializer < Spree::Api::V2::BaseSerializer
  set_type: :video
  
  attributes :url
end
```

Now in your `app/serializers/my_product_serializer.rb`

```ruby
class MyProductSerializer < Spree::V2::Storefront::ProductSerializer
  attribute :my_new_custom_attribute
  
  has_many :videos, serializer: :video
end
```

Hitting the Products API you will notice that in the [relationships](https://jsonapi.org/format/#document-resource-object-relationships) key there will be a new key called `videos`

To include Video response in the Product API add `?includes=videos` in the API URL, eg.

```text
https://localhost:3000/api/v2/storefront/products?include=videos
```


---
title: API v2
section: customization
order: 6
description: This page covers customization of both Storefront API and Platform API
---

# API v2

## Customizing existing API endpoints

### Customizing JSON response

Spree uses J[SON API serializers](https://github.com/jsonapi-serializer/jsonapi-serializer) to represent data returned by API endpoints. 

You can easily swap OOTB Spree serializers with your own thanks to [Spree Dependencies](dependencies.md). 

Let's say you want to customize the Storefront API's [Product serializer](https://github.com/spree/spree/blob/master/api/app/serializers/spree/v2/storefront/product_serializer.rb). Let's start with creating a new serializer file in your project's `app/serializers` directory, that is `app/serializers/my_product_serializer.rb`:

```ruby
class MyProductSerializer < Spree::V2::Storefront::ProductSerializer
  attribute :my_new_custom_attribute
end
```

Now let's tell Spree to use this new serializer, in `config/initializers/spree.rb` please set:

```ruby
Spree::Api::Dependencies.storefront_product_serializer = 'MyProductSerializer'
```

Restart the webserver and hit the [Products API ](https://api.spreecommerce.org/docs/api-v2/b3A6MzE0Mjc2Mg-list-of-products)to notice changes.


---
description: >-
  Spree is a modular, API-first headless ecommerce platform which consists of
  several APIs.
---

# Headless Commerce

![Spree architecture](../.gitbook/assets/spree_commerce_spree_api\_3-2x.png)

## Spree APIs

Spree is a modular, API-first headless e-commerce platform that consists of several APIs.

### [Storefront API](https://api.spreecommerce.org/docs/api-v2/YXBpOjMxMjQ5NjA-storefront-api-v2)

* Modern and lightweight REST API based on JSON API schema
* Designed for building Storefronts and mobile apps
* [JavaScript / TypeScript SDK](https://github.com/spree/spree-storefront-api-v2-js-sdk) available
* [Next.js Commerce integration](../storefronts/next.js-commerce.md) available [🎉](https://emojipedia.org/party-popper/)
* [Vue Storefront integration](../storefronts/vue-storefront.md) available [🚀](https://emojipedia.org/rocket/)

### [Platform API](https://api.spreecommerce.org/docs/api-v2/YXBpOjg3MzkxODk-platform-api-v2) (Developer Preview)

![](../.gitbook/assets/spree_commerce_spree_api\_6.png)

* OAuth 2.0 authentication
* designed for building application to application integration
* permission sets based access to resources
* access any resource on the Spree platform and perform any action

### Webhooks

We're working hard to deliver webhooks in the [Spree v4.4](https://github.com/spree/spree/milestone/45)!

## Storefronts

Spree allows limitless storefront customization. 

You can build your own storefront from scratch using our [SDK](https://github.com/spree/spree-storefront-api-v2-js-sdk) which takes care of all heavy lifting tasks, or you can use [Next.js Commerce](../storefronts/next.js-commerce.md) or [Vue Storefront](https://www.vuestorefront.io). 

## Spree modules

Spree is divided into several modules / ruby gems which you can install independently. 

{% hint style="info" %}
[Spree Starter ](https://github.com/spree/spree_starter)comes with all modules pre-installed for your convenience!
{% endhint %}

| Spree module      | Description                                  |
| ----------------- | -------------------------------------------- |
| **spree**         | Data models, Services and APIs               |
| **spree_backend** | Admin Panel UI                               |
| **spree_sample**  | Sample seed data                             |
| **spree_emails**  | Transactional emails, eg. order confirmation |

There are many other packages adding more features called [Extensions](../extensions/extensions.md).

To change which Spree gems you would like to install you will need to modify your project `Gemfile`.

### Headless installation (default)

```ruby
gem 'spree'
```

### Headless with Admin Panel

```ruby
gem 'spree'
gem 'spree_backend'
```

After changing the `Gemfile` you need to run

```bash
bundle install
```

or if using [Spree Starter](https://github.com/spree/spree_starter):

```bash
bundle install
docker-compose build
```


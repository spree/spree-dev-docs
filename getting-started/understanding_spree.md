---
title: Understanding Spree
section: getting_started
order: 1
---

# Understanding how Spree works

## Headless Commerce

Spree is a modular, API-first headless commerce application. What does it mean? 

Spree comes with a set of [APIs](https://api.spreecommerce.org/) you can work with directly or via [SDK](https://github.com/spree/spree-storefront-api-v2-js-sdk) to build your own Storefront.

For application to application integration, you can use Platform API.

There are optional Admin / Storefront packages available also.

## Spree codebase

Spree API is written in Ruby on Rails framework and is mounted into a Rails application as [a Rails Engine](https://guides.rubyonrails.org/engines.html).

You don't need to be a Rails developer to work with Spree. You can install Spree via Spree Starter or Docker and not touch the underlying codebase at all and work only with the APIs. 

### Spree namespace

All Spree models, controllers and other Ruby classes are namespaced by the `Spree` keyword, eg. `Spree::Product`. This means that those files are also located in `spree` sub-directories eg. [app/models/spree/product.rb](https://github.com/spree/spree/blob/master/core/app/models/spree/product.rb).

### Spree modules

Spree is divided into several modules / gems which you can install independently. 

Installing Spree via [Spree Starter](https://github.com/spree/spree_starter) gives you access to all of Spree features such as Storefront, API and Admin Panel. 

| Spree module | Description |
| :--- | :--- |
| **spree** | Data models, Services and APIs |
| **spree\_backend** | Admin Panel UI \(Rails\) |
| **spree\_frontend** | Storefront \(Rails\) |
| **spree\_sample** | Sample seed data |

--

There are many other Spree-gems providing additional functionality to your Store called [Extensions](https://github.com/spree/spree-dev-docs/tree/0628094f68853238d9b13aa3b24d7b1e1b13fca4/extensions/README.md).

To change which Spree gems you would like to install you will need to modify your project `Gemfile`.

### Headless installation \(default\)

```ruby
gem 'spree'
```

### Admin Panel

```ruby
gem 'spree'
gem 'spree_backend'
```

### Storefront and Admin Panel

```ruby
gem 'spree'
gem 'spree_backend'
gem 'spree_frontend'
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

## Next steps

We recommend you go over [Internals section](../internals/stores.md) to learn more about how Spree works under the hood.


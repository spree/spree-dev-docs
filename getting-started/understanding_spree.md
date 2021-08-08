---
title: Understanding Spree
section: getting_started
order: 1
---

# Understanding how Spree works

Spree is a modular application with a lean core, REST API and 

## Rails Engine

Spree is a [Ruby on Rails Engine](https://guides.rubyonrails.org/engines.html), which means it's an application that provides functionality to their host applications \(that is your store application\).

Spree is a collection of Models, Views and Controllers that your application gains access when you install Spree. You can easily combine Spree with any Ruby on Rails application meaning you can add e-commerce capabilities to your existing RoR applications.

## Spree namespace

All Spree models, controllers and other classes are namespaced by the `Spree` keyword, eg. `Spree::Product`. This means that those files are also located in `spree` sub-directories eg. [app/models/spree/product.rb](https://github.com/spree/spree/blob/master/core/app/models/spree/product.rb).

## Spree modules

Spree is divided into several modules / gems which you can opt-out if you would like. Installing Spree via Spree Starter gives you access to all of Spree features such as Stoprefront, API and Admin Panel. Not all of the modules are required, eg. headless installations will not require Storefront at all.

| Spree module | Description | Required? |
| :--- | :--- | :--- |
| **api** | REST API for | **yes** |
| **backend** | Admin Panel UI | no |
| **core** | Data models, Services and libraries | **yes** |
| **frontend** | Storefront UI | no |
| **sample** | Sample seed data | no |

--

There are many other Spree-gems providing additional functionality to your Store called [Extensions](/extensions).

To change which Spree gems you would like to install you will need to modify your project `Gemfile`.

### Headless installation

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

After changing `Gemfile` please run

```bash
bundle install
```

or if using [Spree Starter](https://github.com/spree/spree_starter):

```bash
bin/bundle-install
```

## Next steps

We recommend you go over [Internals section](../internals/stores.md) to learn more how Spree works under the hood. This knowledge will be very helpful when you'll decide you want to [customize your Spree store](../customization/dependencies.md).


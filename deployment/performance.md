---
description: >-
  This guide will cover all sorts of topics related to Spree application
  performance
---

# Performance

## Application

### API

#### OJ gem

We strongly recommend adding [OJ gem](https://github.com/ohler55/oj) to your application. 

If you're using [Spree Starter](https://github.com/spree/spree_starter) this gem is already pre-installed and pre-configured. If you're not using Spree Starter you can easily add it yourself - please see this [git commit](https://github.com/spree/spree_starter/commit/e50973be8e8833f5d6eeaa0226f322746a860cd2).

#### Caching configuration

There are several configuration options you can put in `config/initializers/spree.rb` to adjust API caching configuration:

```ruby
Spree::Api::Config[:api_v2_cache_ttl] = 3600 # TTL for cached resources in seconds
```

This is the time when API objects will be available in cache storage. Objects such as Products also auto-expire when they are updated or one of their associated resources \(eg. Variants\) are updated also. 

### Background jobs

Sending emails, parsing big amounts of data - it's not recommended to do it in the web process. 

We recommend setting up [Sidekiq with ActiveJob](https://github.com/mperham/sidekiq/wiki/Active-Job), this required a Redis instance. Spree Starter users don't need to do anything as it's already pre-configured for them.

### Testing locally

To enable caching in the development environment please type in your project directory:

```bash
bin/rails dev cache
```

or if you're using Spree Starter

```bash
docker-compose run web rails dev:cache
```

After that, you will need to restart your webserver / or stop/start docker-compose.

## Infrastructure

### Cache storage engine

We strongly recommend using Memcached or Redis as cache storage. 

#### Spree Starter

Starter is pre-configured to work with Memcached. To enable caching please set the ENV variables:

`MEMCACHEDCLOUD_SERVERS` - URL of the Memcached instance

`MEMCACHEDCLOUD_USERNAME` / `MEMCACHEDCLOUD_PASSWORD` - username/password required to access instance

`MEMCACHED_POOL_SIZE` - connection pool, defaults to `5` 

#### Memcached

Please see the configuration options [detailed in Rails Guides](https://guides.rubyonrails.org/caching_with_rails.html#activesupport-cache-memcachestore).

#### Redis

Please see the configuration options [detailed in Rails Guides](https://guides.rubyonrails.org/caching_with_rails.html#activesupport-cache-rediscachestore).

### 


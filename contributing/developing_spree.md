---
description: >-
  This guide covers all the necessary steps to contributing to Spree source
  code. We're happy you're here!
---

# Developing Spree

## Spree codebase

Spree API is written in Ruby on Rails framework and is mounted into a Rails application as [a Rails Engine](https://guides.rubyonrails.org/engines.html).

You don't need to be a Rails developer to work with Spree. You can install Spree via Spree Starter or Docker and not touch the underlying codebase at all and work only with the APIs.&#x20;

### Spree namespace

All Spree models, controllers and other Ruby classes are namespaced by the `Spree` keyword, eg. `Spree::Product`. This means that those files are also located in `spree` sub-directories eg. [app/models/spree/product.rb](https://github.com/spree/spree/blob/master/core/app/models/spree/product.rb).

## Forking Spree repo

Go to [Spree GitHub repository](https://github.com/spree/spree) and click **Fork** button. This will create a copy of Spree repository on your GitHub account. See [Github Documentation](https://docs.github.com/en/github/getting-started-with-github/fork-a-repo) for more information on forking.

## Local setup

1.  Clone your fork repository

    ```
     git clone git://github.com/your_github_username/spree.git
     cd spree
    ```
2. [Install ruby](https://www.ruby-lang.org/en/documentation/installation/)
3.  Install required libraries

    ```
    /bin/bash -c "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/HEAD/install.sh)" && brew install openssl mysql postgresql imagemagick redis
    ```
4.  Install the gem dependencies

    ```
     bundle install
    ```

## Create Sandbox application

Bellow command will setup a Rails application with Spree pre-installed with some data seeded:

```
bundle exec rake sandbox
```

By default, Sandbox uses the **PostgreSQL** database. But you can switch to **MySQL**:

```
DB=mysql bundle exec rake sandbox
```

Start the server

```
cd sandbox
bin/rails s
```

### Performance in development mode

You may notice that your Spree store runs slower in development environment. This is caused by disabled caching and automatic reloading of code after each change.

### Caching

Caching is disabled by default. To turn on caching please run:

```bash
bin/rails dev:cache
```

You will need to restart rails server after this change.

## Making changes

Create a new branch for your changes. Do not push changes to the main branch. Branch name should be human-readable and informative, eg.

* bug fixes: `fix/order-recalculation-total-bug`
* features: `feature/my-new-amazing-feature`

## Running Tests

We use [CircleCI](https://circleci.com) to run the tests for Spree.

You can see the build statuses at [https://circleci.com/gh/spree/spree](https://circleci.com/gh/spree/spree).

Each gem contains its own series of tests, and for each directory, you need to do a quick one-time creation of a test application and then you can use it to run the tests. For example, to run the tests for the core project.

```
cd core
bundle exec rake test_app
bundle exec rspec
```

If you would like to run specs against a particular database you may specify the dummy app's database, which defaults to sqlite3.

```
DB=postgres bundle exec rake test_app
```

If you want to run specs for only a single spec file

```
cd core
bundle exec rspec spec/models/spree/state_spec.rb
```

If you want to run a particular line of spec

```
cd core
bundle exec rspec spec/models/spree/state_spec.rb:7
```

### Running integration tests on MacOS (only applicable for Admin Panel)

We use chromedriver to run integration tests. To install it please use this command:

```bash
brew cask install chromedriver
```

## Submitting Changes

Please keep your commit history meaningful and clear. [This guide](https://about.gitlab.com/blog/2018/06/07/keeping-git-commit-history-clean/) covers it quite well and we recommend reading it, not only for Spree project but for any IT project overall.

1.  Push your changes to a topic branch in your fork of the repository.

    ```
     git push -u origin fix/order-recalculation-total-bug
    ```
2.  Create a Pull request - [please follow this guide](https://docs.github.com/en/github/collaborating-with-issues-and-pull-requests/creating-a-pull-request-from-a-fork)

    If your changes references Github issues, please mark which issue you're fixing by adding `Fixes #<number or url of the issue>` in the commit name or PR title/description. This will automatically mark that issue as closed when your PR will be merged.
3. Wait for CI to pass
4.  If CI passed wait for Spree Core team code review

    We're aiming to review and leave feedback as soon as possible. We'll leave you a meaningul feedback if needed.

## That's a wrap!

Thank you for participating in Open Source and improving Spree - you're awesome!

# Installation

## Prerequisites

Before proceeding make sure you have [Ruby](https://www.ruby-lang.org/en/) installed on your system. This is fairly straightforward but differs depending on which operating system you use.

If you would like to add Spree to your existing Ruby on Rails application, please [follow this guide instead](../advanced/existing\_app\_tutorial.md) (for advanced users).

### Windows

Windows users will need to [install Windows Subsystem for Linux](https://docs.microsoft.com/en-us/windows/wsl/install-win10) to proceed.

## Installation

1. Download [Spree Starter](https://github.com/spree/spree\_starter/archive/main.zip)
2. Unzip it
3. Rename `spree_starter-main` directory as you please
4. Run `bin/setup` in said directory
6. Run `bin/rails s` to start the web server

## Hello, Spree Commerce

You now have a functional Spree application after running only a few commands!

To stop the web server, hit `Ctrl-C` in the terminal window where it's running.&#x20;

### Logging Into the Admin Panel

The next thing you'll probably want to do is to log into the admin interface. Use your browser window to navigate to [http://localhost:3000/admin](http://localhost:3000/admin). You can log in with the username `spree@example.com` and password `spree123`.

Upon successful authentication, you should see the admin screen:

![](../.gitbook/assets/admin\_panel\_978-2x.jpg)

Feel free to explore some of the Admin Panel features that Spree has to offer and to verify that your installation is working properly.

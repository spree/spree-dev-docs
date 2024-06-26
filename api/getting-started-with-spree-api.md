# Getting Started with Spree API

Spree comes with a fully-featured API that allows it to operate in a fully headless mode (if you wish). This means that you can use Spree as a backend for your custom storefront, mobile app, or any other application that needs to interact with an e-commerce platform.

To use the APIs, install the `spree_api` gem with a version corresponding to your version of Spree. If you're using [spree\_starter](https://github.com/spree/spree\_starter) as a base for your project or you have the `spree` gem in your `Gemfile` the API will be included out of the box.

Currently there are two types of APIs:

* [Storefront API](storefront-api/) - that's designed to allow customers to interact with the store via external applications (e.g. Vue Storefront or a dedicated mobile app).
* [Platform API](platform-api/) - that provides management capabilities, allowing third party apps to perform actions otherwise available via the admin panel.

Spree also offers a legacy v1 API, that's been extracted to `spree_api_v1` gem in Spree 4.5. It is not recommended to use it in new projects, but it's still available for existing ones.

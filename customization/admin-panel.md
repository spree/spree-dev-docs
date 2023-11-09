# Admin Panel

Starting with Spree 4.7, we've introduced a new way of customizing the admin panel, that enables extensions to modify the admin panel UI without depending on the Deface gem. For Spree 4.6 and earlier, please see how to use [deface\_overrides\_tutorial.md](../advanced/deface\_overrides\_tutorial.md "mention") overrides.

### Customizing the main menu

When extending Spree with custom features, it's common to add new options to the menu on the left-hand side.&#x20;

The menu is built with [`Spree::Admin::MainMenu::Section`](https://github.com/spree/spree\_backend/blob/main/app/models/spree/admin/main\_menu/section.rb) and [`Spree::Admin::MainMenu::Item`](https://github.com/spree/spree\_backend/blob/main/app/models/spree/admin/main\_menu/item.rb) objects.&#x20;

Additionally, there are two builder classes [`Spree::Admin::MainMenu::SectionBuilder`](https://github.com/spree/spree\_backend/blob/main/app/models/spree/admin/main\_menu/section\_builder.rb) and [`Spree::Admin::MainMenu::ItemBuilder`](https://github.com/spree/spree\_backend/blob/main/app/models/spree/admin/main\_menu/item\_builder.rb) that make it easier to build more complex sections.

The menu is available under `Rails.application.config.spree_backend.main_menu` and can be modified by both extensions as well as the Rails application code.



Example: adding an additional section to the admin panel:

```ruby
Rails.application.config.after_initialize do
    Rails.application.config.spree_backend.main_menu.add(
      Spree::Admin::MainMenu::SectionBuilder.new('subscriptions', 'inbox-fill.svg').
         with_admin_ability_check(Spree::Subscription).
         with_items(
           Spree::Admin::MainMenu::ItemBuilder.new('active', Spree::Core::Engine.routes.url_helpers.admin_active_subsciptions_path).build,
           Spree::Admin::MainMenu::ItemBuilder.new('expired', Spree::Core::Engine.routes.url_helpers.admin_expired_subsciptions_path).build
         ).
         build
    )
end
```

For a more extensive example, take a look at how the [default menu is built](https://github.com/spree/spree\_backend/blob/main/app/models/spree/admin/main\_menu/default\_configuration\_builder.rb).

### Customizing existing views and partials

If you need a more extensive customization of any of the admin panel pages, you can just copy their .erb file from the `spree_backend` gem to your `app/views/` directory and modify it there. This allows you to fully override default views provided by the `spree_backend` gem.

Note: This approach is not recommended for Spree extensions, as it may conflict with other extensions that modify the same view.


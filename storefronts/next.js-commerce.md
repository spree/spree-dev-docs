# Next.js Commerce

[Next.js Commerce](https://nextjs.org/commerce) is an all-in-one React starter kit for high-performance ecommerce sites.

![](../.gitbook/assets/screenshot-2021-09-14-at-22.45.58.png)

See the live demo: [https://spree.vercel.app/](https://spree.vercel.app/)

### Installation

1. Clone the git repository

   ```text
   git clone git@github.com:spree/nextjs-commerce.git
   ```

2. Copy the `.env.template` file in this directory \(`/framework/spree`\) to `.env.local` in the main directory

   ```text
   cp framework/spree/.env.template .env.local
   ```

3. Set `NEXT_PUBLIC_SPREE_CATEGORIES_TAXONOMY_PERMALINK` and `NEXT_PUBLIC_SPREE_BRANDS_TAXONOMY_PERMALINK` environment variables:
   * They rely on [taxonomies'](https://dev-docs.spreecommerce.org/internals/products#taxons-and-taxonomies) permalinks in Spree.
   * Go to the Spree admin panel and create `Categories` and `Brands` taxonomies if they don't exist and copy their permalinks into `.env.local` in NextJS Commerce.
4. Finally, run `yarn dev` 🎉


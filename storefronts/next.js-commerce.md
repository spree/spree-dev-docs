# Next.js Commerce

[Next.js Commerce](https://nextjs.org/commerce) is an all-in-one React starter kit for high-performance e-commerce sites.

![](../.gitbook/assets/screenshot-2021-09-14-at-22.45.58.png)

See the live demo: [https://spree.vercel.store/](https://spree.vercel.store/)

### Installation

1. Clone the git repository:

   ```text
   git clone https://github.com/spree/nextjs-commerce.git
   ```

2. Copy the `framework/spree/env.template` file to `.env.local` in the main directory:

   ```text
   cp framework/spree/.env.template .env.local
   ```

3. Adjust the `NEXT_PUBLIC_SPREE_CATEGORIES_TAXONOMY_PERMALINK` and `NEXT_PUBLIC_SPREE_BRANDS_TAXONOMY_PERMALINK` environment variables inside `.env.local`:
   * They rely on [taxonomies'](https://dev-docs.spreecommerce.org/internals/products#taxons-and-taxonomies) `permalink` values set in Spree.
   * Go to the Spree admin panel and create `Categories` and `Brands` taxonomies if they don't exist. Copy their permalinks into `.env.local` in NextJS Commerce.
4. Finally, run `npm install` and `npm run dev`.


# Spree CLI

Spree CLI is a tool that makes it easy to bootstrap a new Spree project. It provides an interactive process for configuring Spree backend (running in Dockerized, Hybrid or Native mode) and a selection of available frontends.

### Usage

To get started, simply run the following command in your terminal:

```bash
npx @spree/cli new app
```

This will launch the interactive process that will guide you through the process of setting up a new Spree-based store.

In order to start the already generated app, navigate to your project's folder and run the following command:

```bash
npx @spree/cli start app
```

Happy hacking!



### Dependencies

Node 14+ is required to run the CLI. Depending on the chosen Spree setup, you will have to install different dependencies first:

#### Spree (dockerized)

* docker >= 20.0
* docker-compose

#### Spree (no docker)

* ruby = 3.0.3
* vips >= 8.6
* gpg
* psql
* redis

#### Spree (hybrid)

* docker >= 20.0
* docker-compose
* ruby = 3.0.3
* vips >= 8.6
* redis (only needed for running rspec tests)

#### Vue Storefront

* node >= 14.15 <= 14.19
* yarn

#### Next.js Commerce

* node >= 13.0
* yarn

### Running the CLI locally (debugging / contributing)

If you want to make some custom changes to how the CLI works or contribute to it, you will need to run it locally. To do so, first clone the [repo](https://github.com/spree/spree\_cli):

```
git clone https://github.com/spree/spree_cli.git
```

Install all the dependencies:

```
cd spree_cli && yarn
```

Build the CLI:

```
yarn build
```

When the build process is finished you should be able to execute the CLI using local scripts instead of npx:

```
./bin/run new app
```

And start up the existing project with:

```
cd project-folder && ./../bin/run start app
```

### Troubleshooting

#### 1. NextJS storefront doesn't start properly

If the Storefront doesn't start you need to relaunch server manually. To do so you should navigate to `/integration` folder inside created project and type `yarn dev` into console.

#### 2. NextJS storefront stops during launch

In case if the server is randomly stopping during launch it is advised to stop it (for example with `ctrl + c`) and repeat steps mentioned above.

If you have encountered any other problem with NextJS you can also refer to NextJs docs: [https://github.com/vercel/commerce](https://github.com/vercel/commerce)

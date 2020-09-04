# Vue, Gridsome, Strapi

Project to become familiar with Gridsome and Strapi

[Gridsome Docs](https://gridsome.org/)
[Strapi Docs](https://strapi.io/)

## Strapi API Generator

To work with Strapi `cd` to the project root and enter one of these commands:

```sh
yarn strapi develop
yarn strapi start
yarn strapi build
yarn strapi
```

After running `yarn strapi develop`, the Strapi admin panel is available at `localhost:1337`. Depending on DB permissions, the API can be queried in a browser at `localhost:1337/<collection-name>/<collection-id>`

## Gridsome Static Site Generator

To work with Gridsome `cd` to the folder and run either of these commands:

```sh
gridsome develop
gridsome build
```

After running `gridsome develop`, a live-reload view is available at `localhost:8080`, as well as a GraphQL playground at `localhost:8080/___explore`

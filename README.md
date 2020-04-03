# nuxt-github-pages

> Nuxt Example for Github Pages

This repo is to serve as a configuration example of a Nuxt app for hosting on Github Pages.

Github Pages is an easy, integrated way to host a Github project with Nuxt. However, there are some common configuration pitfalls you want to avoid due to how Github Pages and Nuxt work.

The Nuxt documentation has a [pretty decent guide](https://nuxtjs.org/faq/github-pages/) on how to your Nuxt app up and running on Github Pages but it does seem to neglect a few issues that I ran into with a recent project update. These issues crop up if you are using SSR ('universal' mode).

- If you refresh any page but the home page, you get a 404.

This drove me crazy for awhile as I couldn't find a straight answer. Most answers I found in Nuxt Github issues stated this was due to the base route not being configured correctly for Github Pages but I had made sure that was not the case.

In `nuxt.config.js`:

```javascript
// only add `router.base = '/<repository-name>/'` if `DEPLOY_ENV` is `GH_PAGES`
const routerBase =
  process.env.DEPLOY_ENV === 'GH_PAGES'
    ? {
        router: {
          base: '/<repository-name>/'
        }
      }
    : {}

export default {
  ...routerBase
}
```

In `package.json`:

```javascript
"scripts": {
  "build:gh-pages": "DEPLOY_ENV=GH_PAGES nuxt build",
  "generate:gh-pages": "DEPLOY_ENV=GH_PAGES nuxt generate"
},
```

- Note: Windows users may need to install an npm package called cross-env
  `npm install cross-env --save-dev`
  Then prepend `cross-env` to the build and generate scripts:

```javascript
  "build:gh-pages": "cross-env DEPLOY_ENV=GH_PAGES nuxt build",
  "generate:gh-pages": "cross-env DEPLOY_ENV=GH_PAGES nuxt generate"
```

Assets not found (Nuxt build and generate workflow)

404 on refresh (conditional spa mode, generate fallback)

Seperate branches for dev vs github pages config

## Build Setup

```bash
# install dependencies
$ npm install

# serve with hot reload at localhost:3000
$ npm run dev

# build for production and launch server
$ npm run build
$ npm run start

# generate static project
$ npm run generate
```

For detailed explanation on how things work, check out [Nuxt.js docs](https://nuxtjs.org).

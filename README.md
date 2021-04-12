# Nitro does not respect module path (e.g. in monorepo) with target: server

Hey all!

When using Nitro with `target: server` and a monorepo (see repo structure), the Nitro output does not include the correct path to the deps (e.g. un fetch polyfill)


## Repo

1. Install deps `yarn`
2. Build app `yarn build`
3. Check `packages/app/.output/server/index.js`. Here, the path is set correct (`../../../../node_modules/@nuxt/un/runtime/polyfill/fetch.node.js` in our case)
4. Now check `packages/app/.output/server/nitro/server.js`. The path **incorrect** here
5. Same for `packages/app/.output/server/nitro/chunks/app/render.js`

Expected path: `require('../../../../../node_modules/@nuxt/un/runtime/polyfill/fetch.node.js');`
Actual path: `require('../../../../node_modules/@nuxt/un/runtime/polyfill/fetch.node.js');`

When fixing the paths manually, the app runs as expected

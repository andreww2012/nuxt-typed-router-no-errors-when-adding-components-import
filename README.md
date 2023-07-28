# Steps to reproduce

## Preparation

* Install dependencies: `pnpm i`
* This will run then post-install script (`nuxt prepare`) that will generate `.nuxt` directory contents which includes TS types

## Bug reproduction

* Run `pnpm test` - expected to find errors
* Go to `app.vue` and uncomment any of the imports there.
* Run `pnpm test` - still expected to find errors
* Run `pnpm dev` (launches Nuxt in dev mode)
* This will slightly modify `.nuxt` directory, namely a `NuxtLink` entry will be added to `.nuxt/components.d.ts` which will cause the bug in question in the next step:

```patch
--- a/.nuxt/components.d.ts
+++ b/.nuxt/components.d.ts
@@ -8,7 +8,7 @@ declare module 'vue' {
     'ClientOnly': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/app/components/client-only")['default']
     'DevOnly': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/app/components/dev-only")['default']
     'ServerPlaceholder': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/app/components/server-placeholder")['default']
-    
+    'NuxtLink': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/app/components/nuxt-link")['default']
     'NuxtLoadingIndicator': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/app/components/nuxt-loading-indicator")['default']
     'NuxtPage': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/pages/runtime/page")['default']
     'NoScript': typeof import("../node_modules/.pnpm/nuxt@3.6.5_@types+node@18.17.0_typescript@5.1.6_vue-tsc@1.8.8/node_modules/nuxt/dist/head/runtime/components")['NoScript']
```

* Run `pnpm test` and it won't find any errors now.
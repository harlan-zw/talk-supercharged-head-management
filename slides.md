---
theme: ./theme
class: text-center
highlighter: shiki
lineNumbers: false
drawings:
  persist: false
css: windicss
title: Supercharged &lt;head&gt;
---

# Supercharged &lt;head&gt; management

## VueUse head v1 and the future of SEO with Nuxt v3

<div class="opacity-90 text-sm absolute -bottom-2 right-10">A talk by Harlan Wilton <img src="/img.png" class="w-8 h-8 ml-2 rounded-full inline-block" /></div>

<!--
- Welcome everyone, great to be here and see some familiar faces. This is the first meetup I've been too in a long time, so very exciting to talk

- Today I wanted to talk about Vite. Sure you've all heard of it by now.

- cover a brief history building frontend and what the future holds, pivotal moment for the space a lot of exciting things are happening

- I've tried to keep it simple and high level but let me know if you have any questions as we go
-->

---
layout: two-cols
size: lg
---

# About Me

::left::

<v-clicks>

🇦🇺 Sydney based. Open Source dev
- <span class="uppercase text-xs mr-2 opacity-90">Team</span> <logos-vueuse /> VueUse, <windi-icon /> WindiCSS
- <span class="uppercase text-xs mr-2 opacity-90">Contributing</span> <img src="https://nuxt.com/assets/design-kit/logo/icon-green.svg" width="20" height="20" class="h-20px" style="margin: 0; display: inline;"> Nuxt <span class="text-xs opacity-70">(insider)</span>, <logos-vitejs /> Vite <span class="text-xs opacity-70">(ecosystem)</span>
- <span class="uppercase text-xs mr-2 opacity-90">Modules</span> nuxt-windicss, nuxt-webpack-optimisations, nuxt-delay-hydration, nuxt-schema-org, nuxt-unlighthouse

</v-clicks>


::right::


<img src="https://res.cloudinary.com/dl6o1xpyq/image/upload/f_jpg,q_auto:best,dpr_auto/images/harlan-wilton" class="w-50 h-50 rounded mx-auto" />


---
layout: section-center
---

# Let's begin with a question

---
layout: section-center
class: text-center
---

# In Nuxt, what do these have in common?

## HTML Metadata

## Meta Info

## Meta tags

## Head Tags


---
layout: section-center
---

# They're all the same

Managing _machine-readable_ elements and attributes outside the Vue render tree for SSR and DOM.

<v-click>
```html
<html ${htmlAttrs}>
  <head>
    ${headTags}
  </head>
  <body ${bodyAttrs}>
    ${bodyTagsOpen}
    <div id="app">${appHTML}</div>
    ${bodyTagsClose}
  </body>
</html>
```
</v-click>

<v-click>
```ts
const $el = document.createElement(tag)
setAttrs($el, attrs)
```
</v-click>


---
layout: section-center
class: text-center
---

# Can it be named better?

<p class="text-6xl">
<span class="animated animate-pulse">🤔</span>
<span class="animated animate-pulse animate-delay-0.3s">🤔</span>
<span class="animated animate-pulse animate-delay-0.7s">🤔</span>
</p>

---
layout: section-center
class: text-center
---

<img src="/img_14.png" class="max-h-[60%] mx-auto">


---
layout: section-center
class: text-center
---

# Probably

## But it's good enough 🤷

##  useHead -> Head tag management

---
layout: section-center
---

<h1><span class="text-sm"><logos-nuxt-icon /> Nuxt v2</span><div class="mt-3">VueMeta</div></h1> 


```vue
<script>
export default {
  head() {
    return {
      title: 'My page title',
      meta: [ { hid: 'description', name: 'description', content: 'My description' } ]
    }
  }
}
</script>
```


<v-click>

- Built by Nuxt team
- Options API ✅
- Composition API ❌

</v-click>


<!--
- Now let's get into it

- We're going to go back in time and see how we've dealt with bundling over the ages
-->


---
layout: section-center
---

<h1><span class="text-sm"><img src="https://nuxt.com/assets/design-kit/logo/icon-green.svg" width="20" height="20" class="h-20px" style="margin: 0; display: inline;"> Nuxt v3</span><div class="mt-3">VueUse Head</div></h1> 


```vue
<script setup>
useHead({
  title: 'My page title',
  meta: [
    { name: 'description', content: 'My description' }
  ]
})
</script>
```


<v-click>

- Built by EGOIST
- Options API ✅ (Nuxt mixin)
- Composition API ✅

</v-click>

---
layout: section-center
class: text-center
---

# What does being a VueUse composable mean?

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse</span><div class="mt-3">Composables</div></h1> 

Accept reactive arguments: `ref`, `computed` and reactive getter

```ts
const title = ref('My page title')
useHead({ 
  title
})
title.value = 'My new title'
```

<v-click>

Cleans up the side-effects automatically, if it has any.

```ts
onBeforeUnmount(() => sideEffects.dispose())
```

</v-click>

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse</span><div class="mt-3">Quick tip: Avoid wrapping in watchers</div></h1> 


```ts
// ❌ Bad 
watch(ref, () => {
  useHead({ title: ref.value })
})
```


<v-click>
```ts
// ✅ Good 
useHead({ title: () => ref.value })
```

</v-click>


---
layout: section-center
class: text-center
---

# What has been going on with VueUse head?

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head - Updates</span><div class="mt-3">A new maintainer: me</div></h1> 

- I fixed a couple of bugs and did some triage. Got hooked.
- Asked Anthony to take over as maintainer, it worked

<img src="/img_2.png" class="mx-auto w-450px">

---
layout: section-center
class: text-center
---

# ✨ Initial enhancements

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head - Updates</span><div class="mt-3">Fully typed `useHead`</div></h1> 

<video autoplay loop muted class="h-250px mx-auto">
<source src="/FeOu7V_agAQzDZ7.mp4" type="video/mp4">
</video>

Created the zhead package. Focus on types but also common auto-completions.

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head - Updates</span><div class="mt-3">Reactive getter support</div></h1> 

```ts
const { data: page } = await usePage()
useHead({ 
  title: () => page.value.title,
  meta: [
    { name: 'description', content: () => page.value.description }
  ]
})
```

---
layout: section-center
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head - Updates</span><div class="mt-3">Still some issues to solve...</div></h1> 

- `useHead` is not as intuitive as it could be: deduping, classes, merging. Number of issues in GitHub.
- DOM patching algorithm is slow, pollutes DOM with state and is accident-prone

```html
<html data-head-attrs="lang,dir">
<head>
<!-- Render 29 tags -->
<meta name="head:count" content="29">
</head>
<body data-head-attrs="class">
</body>
</html>
```


---
layout: section
class: text-center
---

# <logos-vueuse /> VueUse Head v1

## What's new?

---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">Handling duplicates</div></h1> 

```ts
useHead({
  meta: [
    { /*key: 'image-1',*/ property: 'og:image', content: 'https://example.com/img.png' },
    { /*key: 'image-2',*/ property: 'og:image', content: 'https://example.com/img2.png' }
  ]
})
```

```html
<meta name="og:image" content="https://example.com/img.png">
<meta name="og:image" content="https://example.com/img2.png">
```

Tip: key, hid and vmid are all the same! Use key from now on.

---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">Handling duplicates</div></h1> 

```ts
useHead({
  meta: [
    { 
      name: 'og:image',
      // arrays!
      content: [ 'https://example.com/img.png', 'https://example.com/img2.png' ]
    }
  ]
})
```

```html
<meta name="og:image" content="https://example.com/img.png">
<meta name="og:image" content="https://example.com/img2.png">
```


---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">Class Attribute</div></h1> 

```ts
const darkMode = ref(false)
useHead({
  // object support
  htmlAttrs: {
    class: { dark: () => darkMode, light: () => !darkMode }
  },
  // array support
  bodyAttrs: { class: ['layout-id', 'page-id' ] }
})
```

```html
<html class="dark">
<body class="layout-id page-id">
```


---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">Attribute Merging</div></h1> 

```ts
// app.vue
useHead({ htmlAttrs: { class: 'dark' } })

// pages/index.vue
useHead({ htmlAttrs: { class: 'page-index' } })
```

```html
<html class="dark page-index">
```

---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">New Tag Props</div></h1> 

```ts
useHead({ script: [
  {
    // tagPosition: `bodyOpen`, `bodyClose`, `head`
    tagPosition: 'bodyClose',
    src: 'https://example.com/script.js', async: true
  },
  {
    // tagPriority: move tags around
    tagPriority: 'critical', // 'high' , 'low'
    src: 'https://example.com/script2.js'
  },
  {
    // add attributes to existing tags instead of replacing them
    tagDuplicateStrategy: 'merge',
    ['data-foo']: 'bar', key: 'special-script'
  }
]})
```

---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">Prop Promises</div></h1> 

```vue
<script setup>
// returns a Promise when called, normally would need to await it
const fetchUserStyles = async () => (await useFetch('/api/userStyles')).data

useHead({
  // awaited when we render, don't block the page
  style: [{ children: fetchUserStyles() } ]
})
</script>
```


---
layout: section
---

<h1><span class="text-sm"><logos-vueuse /> VueUse Head v1 - More intuitive useHead</span><div class="mt-3">DOM event handlers</div></h1> 

```ts
const stripeLoaded = ref(false)
useHead({
  script: [
    { src: 'https://js.stripe.com/v3/', onload: () => { stripeLoaded.value = true } }
  ],
})
```


```ts
const windowSize = ref({ width: 0, height: 0 })
useHead({
  bodyAttrs: {
    onresize: (e) => { windowSize.value = { width: e.target.innerWidth, height: e.target.innerHeight } }
  }
})
```

---
layout: section
---

# <span class="text-sm"><logos-vueuse /> VueUse Head v1 - DOM patching algorithm</span><div class="mt-3"><fluent-triangle-16-regular /> unhead</div>

<v-clicks>

- New engine powering VueUse Head v1, now part of UnJS.
- Side-effect based: less aggressive removal of tags and attributes. No more non-essential state in DOM
- ⚡ DOM rendering optimisations, 5x faster (~10ms for an avg site)
- Powered by hookable. Same hook system as Nuxt, completely adaptable!

</v-clicks>

---
layout: section
---

# <span class="text-sm"><logos-vueuse /> VueUse Head v1 - Untapped DX</span><div class="mt-3">Server Only Tags</div>

```ts
useServerHead({
  link: [
    { rel: 'icon', type: 'image/png', sizes: '16x16', href: import('~/assets/favicon.png?url') }
  ]
})
```

<v-clicks>

- Support rendering tags which can only be done on the server (imports)
- Move towards 0kb runtime overhead (needs more work)
- Official Nuxt support coming soon

</v-clicks>

---
layout: section
class: text-center
---

# What about making SEO easier?

---
layout: section
---

# <span class="text-sm"><logos-vueuse /> VueUse Head v1 - Untapped DX</span><div class="mt-3">useSeoMeta</div>

```ts
useSeoMeta({
  ogImage: 'https://harlanzw.com/og.png',
  ogUrl: 'https://harlanzw.com',
  twitterSite: '@harlan-zw',
  viewport: { width: 'device-width',  initialScale: 1, userScalable: 'yes' }
})
```

<v-clicks>

- Over 100+ definitions, powered by zhead
- Intended to be treeshaken from client build
- Official Nuxt support coming soon (use now with manual imports)

</v-clicks>

---
layout: section
---

# <span class="text-sm"><logos-vueuse /> VueUse Head v1 - Untapped DX</span><div class="mt-3">InferSeoMetaPlugin</div>

```ts
// will be able to hook into this soon
createHead({ plugins: [ 
    InferSeoMetaPlugin({ ogTitle: (title) => title.replace(' - My Site', '') })
]})
useHead({ title: 'Welcome - My Site' })
useSeoMeta({ description: 'Welcome to my site', ogImage: 'https://example.com/image.jpg' })
```

```html
<title>Welcome - My Site</title>
<meta property="og:title" content="Welcome">
<meta name="description" content="Welcome to my site">
<meta property="og:description" content="Welcome to my site">
<meta property="og:image" content="https://example.com/image.jpg">
<meta property="twitter:card" content="summary_large_image">
<meta name="robots" content="index, follow, max-image-preview:large, max-snippet:-1, max-video-preview:-1">
```

---
layout: section
class: text-center
---

# How can I use this right now?


---
layout: section-center
---


# nuxt-unhead 

_(prev. nuxt-hedge)_

Get early access to experimental features that may or may not land in Nuxt v3.

Everything you just saw, plus:
- 🖥️ True 0kb runtime tags with `useServerHead` and `useSeoMeta`
- 🌳 Augmented types for auto-completion of your files on `href` and `src`
- 📦 Load your asset files directly using aliases

```ts
useHead({ link: [ { href: '~/assets/style.css', as: 'stylesheet', type: 'text/css' }]})
```

github.com/harlan-zw/nuxt-unhead

---
layout: section-center
---

# What's next?

- 0kb runtime overhead for tags if you don't use `useHead` (save around ~5kb gzipped)
- Many nuxt PRs


---
layout: section-center
---

# Practical Nuxt v3 SEO tips 

If you came to my talk for that 🙃

Performance
- Nuxt server components
- nuxt-fontaine
- @nuxtjs/partytown
- @nuxtjs/critters
- unlighthouse (scan your site)

SEO
- nuxt-schema-org
- Maybe something in the works

---
layout: section-center
---

# Thanks!

- Shoutout to antfu, Alexander Lichter, Daniel Roe, Pooya

## Learn More

- Docs at: unhead.harlanzw.com

## Follow me

<div class="opacity-85 text-sm mt-10">Twitter: @harlan_zw</div>

<div class="opacity-85 text-sm mt-3">GitHub: @harlan-zw</div>

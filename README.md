![](https://i.imgur.com/j8tDCOZ.png)

# Vitepress Simple Search

Vitepress needs better offline search. Let's make it simple and quick.

Thanks to everyone in [this thread for offline search](https://github.com/vuejs/vitepress/issues/670) for getting the general idea implemented.

## Features

* Utilizes front-matter for page titles.
* Auto-strips content of extra tags.
* Auto-reads all markdown documents, and creates search data based on that.
* Ability to change baseURL for doc pathing.
* Ability to change regexp for content stripping and searching content.
* Ability to use quotes for stricter search results in-search.

## Required

Make sure all of your markdown documents have `title` in their front matter.

Example:

```md
---
title: 'My Cool Document'
---

# {{ $frontmatter.title }}

Content, and everything else...
```

## Installing

```js
npm i vitepress-plugin-simple-search
```

## Add the plugin

Create a file in `docs` called `vite.config.js` or `vite.config.ts`.

```js
// docs/vite.config.js
import { SearchPlugin } from "vitepress-plugin-simple-search";
import { defineConfig } from "vite";

export default defineConfig({
  plugins: [SearchPlugin()],
});
```

## Additional Options

These can be passed through the `SearchPlugin` function.

```ts
export interface Options {
    /**
     * Base URL to use for content link replacement.
     *
     * @type {string}
     * @memberof Options
     */
    baseURL?: string;

    /**
     * Used as a regex content remover for non-matching characters.
     * Setting this to undefined turns off all content stripping.
     * May have unintended side effects.
     *
     * @type {RegExp | undefined}
     * @memberof Options
     */
    regexForContentStripping?: RegExp | undefined;
}
```

**Example**

```ts
SearchPlugin({ baseURL: '/my-repo', regexForContentStripping: undefined });
```

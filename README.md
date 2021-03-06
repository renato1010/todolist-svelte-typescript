_Looking for a shareable component template? Go here --> [sveltejs/component-template](https://github.com/sveltejs/component-template)_

---

# Instructions to create an app like this, todo-list svelte app with typescript

This is a project template for [Svelte](https://svelte.dev) apps. This project use Typescript from start

To create a new project based on this template using [degit](https://github.com/Rich-Harris/degit):

```bash
npx degit sveltejs/template todo-list
cd todo-list
```

_Note that you will need to have [Node.js](https://nodejs.org) installed._

## Using TypeScript

This template comes with a script to set up a TypeScript development environment, you can run it immediately after cloning the template with:

```bash
node scripts/setupTypeScript.js
```

Or remove the script via:

```bash
rm scripts/setupTypeScript.js
```

## Copy .svelte files

Keep the file structure and copy [Todo](src/components/Todo.svelte) and [TodoList](src/components/TodoList.svelte) components to your project

## Get started

Install the dependencies...

```bash
cd todo-list
npm install
```

...then start [Rollup](https://rollupjs.org):

```bash
npm run dev
```

Navigate to [localhost:5000](http://localhost:5000). You should see your app running. Edit a component file in `src`, save it, and reload the page to see your changes.

By default, the server will only respond to requests from localhost. To allow connections from other computers, edit the `sirv` commands in package.json to include the option `--host 0.0.0.0`.

If you're using [Visual Studio Code](https://code.visualstudio.com/) we recommend installing the official extension [Svelte for VS Code](https://marketplace.visualstudio.com/items?itemName=svelte.svelte-vscode). If you are using other editors you may need to install a plugin in order to get syntax highlighting and intellisense.

## Building and running in production mode

To create an optimised version of the app:

```bash
npm run build
```

You can run the newly built app with `npm run start`. This uses [sirv](https://github.com/lukeed/sirv), which is included in your package.json's `dependencies` so that the app will work when you deploy to platforms like [Heroku](https://heroku.com).

## Single-page app mode

By default, sirv will only respond to requests that match files in `public`. This is to maximise compatibility with static fileservers, allowing you to deploy your app anywhere.

If you're building a single-page app (SPA) with multiple routes, sirv needs to be able to respond to requests for _any_ path. You can make it so by editing the `"start"` command in package.json:

```js
"start": "sirv public --single"
```

## Deploying to the web

### With [Vercel](https://vercel.com)

Install `vercel` if you haven't already:

```bash
npm install -g vercel
```

Then, from within your project folder:

```bash
cd public
vercel deploy --name my-project
```

### With [surge](https://surge.sh/)

Install `surge` if you haven't already:

```bash
npm install -g surge
```

Then, from within your project folder:

```bash
npm run build
surge public my-project.surge.sh
```

## Notes when developing with Typescript

In order to use Typescript features(anotations) in your svelte components
you'll need to add the `lang="ts"` attribute to the `<script>` tag

```svelte
<script lang="ts">
  import { createEventDispatcher } from "svelte";
  import { fade } from "svelte/transition";
  const dispatch = createEventDispatcher();
  export let todo: TodoProp;
</script>

```

### export/import type/interface from `.svelte` files

Export:

```svelte
<script context="module" lang="ts">
  export type TodoProp = {
    id: number;
    text: string;
    done: boolean;
  };
</script>
```

Import:

```svelte
<script lang="ts" context="module">
  import type { TodoProp } from "./Todo.svelte";
</script>
```

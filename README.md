# SvelteKitApp Chrome Extension Template

[SvelteKitApp/sveltekitapp-chrome-extension-template](https://github.com/SvelteKitApp/sveltekitapp-chrome-extension-template)

> Репозиторий сгенерирован командой [`npm create @svelte@latest`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Порядок действия по самостоятельному формированию репозитория

- установка пакета сборки [sveltekit-adapter-chrome-extension](https://github.com/michmich112/sveltekit-adapter-chrome-extension)

```bash
$npm i -D sveltekit-adapter-chrome-extension
```

- настройка адаптера сборки

```diff
-import adapter from "sveltekit@adapter-auto";
+import adapter from "sveltekit-adapter-chrome-extension";
...
-		adapter: adapter()
+		// @see https://github.com/michmich112/sveltekit-adapter-chrome-extension
+		adapter: adapter({
+			// default options are shown
+			pages: 'build',
+			assets: 'build',
+			fallback: null,
+			precompress: false,
+			manifest: 'manifest.json'
+		}),
+		appDir: 'app'
 	}
```

- создание `+layout.ts` для включения предварительной генерации страниц(ы) приложения (обязательное требование)

```bash
$echo 'export const prerender = true;' >> ./src/routes/+layout.ts
```

- создание файла `manifest.json`

```bash
$echo '{}' >> ./static/manifest.json
```

- заполнение `manifest.json`

```diff
-{}
+{
+  "manifest_version": 3,
+  "version": "0.0.1",
+  "name": "sveltekitapp-chrome-extension-template",
+  "description": "Шаблон Chrome extension с использованием Sveltekit",
+  "icons": {
+    "32": "favicon.png"
+  },
+  "action": {
+    "default_popup": "index.html",
+    "default_icon": "favicon.png",
+    "default_title": "sveltekitapp-chrome-extension-template"
+  }
+}
```

## Установка `Tailwind CSS` Framework

- установка `Tailwind CSS`

```bash
$npx svelte-add@latest tailwindcss
$npm i
```

## Установка Skeleton

```bash
$npm i -D @skeletonlabs/skeleton
```

- подключение стилей в `src/routes/+layout.svelte`

```diff
# src/routes/+layout.svelte
+// Your selected Skeleton theme:
+import '@skeletonlabs/skeleton/themes/theme-skeleton.css';
+
+// This contains the bulk of Skeletons required styles:
+// NOTE: this will be renamed skeleton.css in the v2.x release.
+import '@skeletonlabs/skeleton/styles/skeleton.css';
+
+// Finally, your application's global stylesheet (sometimes labeled 'app.css')
import '../app.postcss';
```

- изменение конфигурации  `tailwind.config.cjs`

```diff
# tailwind.config.cjs
 const config = {
-	content: ['./src/**/*.{html,js,svelte,ts}'],
+	// 1. Apply the dark mode class setting:
+	darkMode: 'class',
+	content: [
+		'./src/**/*.{html,js,svelte,ts}',
+		// 2. Append the path for the Skeleton NPM package and files:
+		require('path').join(require.resolve('@skeletonlabs/skeleton'), '../**/*.{html,js,svelte,ts}')
+	],

 	theme: {
 		extend: {}
 	},

-	plugins: []
+	plugins: [
+		// 3. Append the Skeleton plugin to the end of this list
+		...require('@skeletonlabs/skeleton/tailwind/skeleton.cjs')()
+	]
 };
```
## Локальная установка расширения

- выполнить сборку

```bash
$npm run  build
```

- открыть в chrome браузере `chrome://extensions/`
- включить режим рразарботчика
- выполнить действие "Загрузить расспакованное расширение"
- выбрать диеруторию `./build`

## Creating a project

If you're seeing this, you've probably already done this step. Congrats!

```bash
# create a new project in the current directory
npm create svelte@latest

# create a new project in my-app
npm create svelte@latest my-app
```

## Developing

Once you've created a project and installed dependencies with `npm install` (or `pnpm install` or `yarn`), start a development server:

```bash
npm run dev

# or start the server and open the app in a new browser tab
npm run dev -- --open
```

## Building

To create a production version of your app:

```bash
npm run build
```

You can preview the production build with `npm run preview`.

> To deploy your app, you may need to install an [adapter](https://kit.svelte.dev/docs/adapters) for your target environment.

<div align="center">
<img title="Svelte" alt="Svelte"  height=48 width=48 src="https://avatars.githubusercontent.com/u/23617963?s=200&v=4"/>
<img title="Tailwind" alt="Tailwind" height=48 width=48 src="https://avatars.githubusercontent.com/u/67109815?s=200&v=4"/>
<img title="Skeleton" alt="Skeleton"  height=48 width=48 src="https://avatars.githubusercontent.com/u/118298875?s=200&v=4"/>
</div>

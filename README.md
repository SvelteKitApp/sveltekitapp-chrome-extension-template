# SvelteKitApp Chrome Extension Template

[SvelteKitApp/sveltekitapp-chrome-extension-template](https://github.com/SvelteKitApp/sveltekitapp-chrome-extension-template)

> Репозиторий сгенерирован командой [`npm create @svelte@latest`](https://github.com/sveltejs/kit/tree/master/packages/create-svelte).

## Порядок действия по самостоятельному формированию репозитория

- установка пакета сборки [sveltekit-adapter-chrome-extension](https://github.com/michmich112/sveltekit-adapter-chrome-extension)

```bash
$npm i -D sveltekit-adapter-chrome-extension
# дополнительная зависимость для работы с TypeScript
$npm i -D @types/chrome
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

- изменение конфигурации `tailwind.config.cjs`

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
$npm run build
# предварительный просмотр сборки на странице браузера
$npm run preview
```

- открыть в chrome браузере `chrome://extensions/`
- включить режим разработчика
- выполнить действие "Загрузить расспакованное расширение"
- выбрать директорию `./build`

## Разработка

- скопировать репозиторий
- установить зависимости

```bash
$npm i
```

- запустить локальной для разработки UI

```bash
npm run dev
# опция для открытия страницы в браузере
npm run dev -- --open
```

## Источники информации

- [developer.chrome.com/docs/extensions/mv3](https://developer.chrome.com/docs/extensions/mv3/declare_permissions/)
- [skeleton.dev](https://www.skeleton.dev)

<div align="center">
<img title="Svelte" alt="Svelte"  height=48 width=48 src="https://avatars.githubusercontent.com/u/23617963?s=200&v=4"/>
<img title="Tailwind" alt="Tailwind" height=48 width=48 src="https://avatars.githubusercontent.com/u/67109815?s=200&v=4"/>
<img title="Skeleton" alt="Skeleton"  height=48 width=48 src="https://avatars.githubusercontent.com/u/118298875?s=200&v=4"/>
</div>

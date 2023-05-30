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

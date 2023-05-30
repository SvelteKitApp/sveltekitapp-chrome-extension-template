<script lang="ts">
	// Your selected Skeleton theme:
	import '@skeletonlabs/skeleton/themes/theme-skeleton.css';

	// This contains the bulk of Skeletons required styles:
	// NOTE: this will be renamed skeleton.css in the v2.x release.
	import '@skeletonlabs/skeleton/styles/skeleton.css';
	// Finally, your application's global stylesheet (sometimes labeled 'app.css')
	import '../app.postcss';
	import { onMount } from 'svelte';
	import { AppBar, AppShell } from '@skeletonlabs/skeleton';

	let environment: string;

	onMount(() => {
		// NOTE: определение окружения выполнения кода
		if (window.chrome && chrome.runtime && chrome.runtime.id) {
			environment = 'Chrome Extension';
		} else {
			environment = 'Development';
		}
	});
</script>

<!-- App Shell -->
<AppShell>
	<svelte:fragment slot="header">
		<!-- App Bar -->
		<AppBar>
			<svelte:fragment slot="lead">
				<strong class="text-xl uppercase">SvelteKitApp | {environment}</strong>
			</svelte:fragment>
			<svelte:fragment slot="trail">
				<a
					class="btn btn-sm variant-ghost-surface"
					href="https://github.com/SvelteKitApp"
					target="_blank"
					rel="noreferrer"
				>
					SvelteKitApp
				</a>
			</svelte:fragment>
		</AppBar>
	</svelte:fragment>
	<!-- Page Route Content -->
	<slot />
</AppShell>

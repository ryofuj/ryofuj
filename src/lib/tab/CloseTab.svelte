<button class="close" on:click={close} title="Close">
	×
</button>

<style>
	button {
		display: grid;
		place-content: center;
		width: 1em;
		height: 1em;
		padding: 1ch;
		margin-right: 0.5ch;

		@apply rounded hover:bg-gray-200;
	}
</style>

<script lang="ts">
	import { tabs, localStore, activeFeaturedSkill } from '$lib/store'
	import { paths } from '$lib/routes'
	import { page } from '$app/stores'
	import { goto } from '$app/navigation'

	export let path
	export let active: boolean

	function close() {
		$tabs = $tabs.filter(tab => tab !== path)
		localStore('tabs', $tabs)

		// update content to first tab or homepage if closed tab was active
		let currentPageDoesntExist = !paths.includes($page.url.pathname)

		if (active || currentPageDoesntExist) {
			goto($tabs[0] || '/')

			$activeFeaturedSkill = null
			localStore('activeFeaturedSkill', $activeFeaturedSkill)
		}
	}
</script>

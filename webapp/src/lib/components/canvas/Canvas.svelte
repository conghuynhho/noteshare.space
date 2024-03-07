<script lang="ts">
	import { writable } from 'svelte/store';
	import {
		SvelteFlow,
		Controls,
		Background,
		BackgroundVariant,
	} from '@xyflow/svelte'
	// 👇 this is important! You need to import the styles for Svelte Flow to work
	import '@xyflow/svelte/dist/style.css';
	import { browser } from '$app/environment';

  let dark: boolean;

  $: getTheme();

  $: {
      if (browser) {
          window.localStorage.setItem('isDarkMode', String(dark));
      }
  }

  async function getTheme() {
      if (browser) {
          const savedMode = window.localStorage.getItem('isDarkMode');
          dark = savedMode ? savedMode === 'true' : false;
          window.localStorage.setItem('isDarkMode', String(dark));
      }
  }

	// We are using writables for the nodes and edges to sync them easily. When a user drags a node for example, Svelte Flow updates its position.
	const nodes = writable([
		{
			id: '1',
			type: 'input',
			data: { label: 'Input Node' },
			position: { x: 0, y: 0 }
		},
		{
			id: '2',
			type: 'default',
			data: { label: 'Node' },
			position: { x: 0, y: 150 }
		}
	]);

	// same for edges
	const edges = writable([
		{
			id: '1-2',
			type: 'default',
			source: '1',
			target: '2',
			label: 'Edge Text'
		}
	]);

	const snapGrid = [25, 25];

</script>


<div class="h-dvh w-dvw">
	<SvelteFlow
		{nodes}
		{edges}
		{snapGrid}
		colorMode="dark"
		fitView
		on:nodeclick={(event) => console.log('on node click', event.detail.node)}
	>
		<Background/>
		<Controls />
	</SvelteFlow>
</div>

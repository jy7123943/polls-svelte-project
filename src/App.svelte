<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import Tabs from './shared/Tabs.svelte';

	// tabs
	let items = ['Current Polls', 'Add new Poll'];
	let activeItem = items[0];

	const tabChange = ({ detail }) => {
		activeItem = detail;
	};
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === items[0]}
		<p>Poll List component goes here</p>
	{:else if activeItem === items[1]}
		<p>new Poll form component goes here</p>
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>

<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import CreatePollForm from './components/CreatePollForm.svelte';
	import Tabs from './shared/Tabs.svelte';

	// tabs
	let items = ['Current Polls', 'Add new Poll'];
	let activeItem = items[0];

	const tabChange = ({ detail }) => {
		activeItem = detail;
	};


	// polls
	let polls = [
		{
			id: 1,
			question: 'Python or JavaScript',
			answerA: 'Python',
			answerB: 'JavaScript',
			votesA: 9,
			votesB: 15,
		},
	];

	const handleAdd = ({ detail }) => {
		polls = [detail, ...polls];
		activeItem = items[0];
	};
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === items[0]}
		<p>Poll List component goes here</p>
	{:else if activeItem === items[1]}
		<CreatePollForm on:add={handleAdd} />
	{/if}
</main>
<Footer />

<style>
	main {
		max-width: 960px;
		margin: 40px auto;
	}
</style>

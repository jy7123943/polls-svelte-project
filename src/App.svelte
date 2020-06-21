<script>
	import Header from './components/Header.svelte';
	import Footer from './components/Footer.svelte';
	import CreatePollForm from './components/CreatePollForm.svelte';
	import PollList from './components/PollList.svelte';
	import Tabs from './shared/Tabs.svelte';

	// tabs
	let items = ['Current Polls', 'Add new Poll'];
	let activeItem = items[0];

	const tabChange = ({ detail }) => {
		activeItem = detail;
	};

	const handleAdd = ({ detail }) => {
		polls = [detail, ...polls];
		activeItem = items[0];
	};

	const handleVotes = ({ detail: { option, id }}) => {
		let copiedPolls = [...polls];
		let upvotedPoll = copiedPolls.find(poll => poll.id === id);

		if (option === 'a') {
			upvotedPoll.votesA++;
		}
		if (option === 'b') {
			upvotedPoll.votesB++;
		}

		polls = copiedPolls;
	};
</script>

<Header />
<main>
	<Tabs {items} {activeItem} on:tabChange={tabChange} />
	{#if activeItem === items[0]}
		<PollList on:vote={handleVotes} />
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

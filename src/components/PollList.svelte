<script>
  import PollStore from '../stores/PollStore.js';
  import PollDetails from './PollDetails.svelte';
</script>

<div class='poll-list'>
  {#each $PollStore as poll (poll.id)}
    <div>
      <PollDetails {poll} on:vote />
    </div>
  {:else}
    <div>Empty polls</div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

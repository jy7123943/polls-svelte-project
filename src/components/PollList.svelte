<script>
  import { fade, slide, scale } from 'svelte/transition';
  import { flip } from 'svelte/animate';
  import PollStore from '../stores/PollStore.js';
  import PollDetails from './PollDetails.svelte';
</script>

<div class='poll-list'>
  {#each $PollStore as poll (poll.id)}
    <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
      <PollDetails {poll} />
    </div>
  {:else}
    <div class='empty' in:fade>Empty polls</div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
  .empty {
    color: #aaa;
    font-size: 18px;
    font-style: italic;
  }
</style>

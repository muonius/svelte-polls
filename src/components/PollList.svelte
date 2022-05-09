<script>
  import PollDetails from "./PollDetails.svelte";
  export let polls = [];
</script>

<!-- invoke casting vote event here, event forwarding -->
<div class="poll-list">
  {#each polls as poll (poll.id)}
    <div>
      <!-- event forwarding to parent -->
      <PollDetails {poll} on:vote />
    </div>
  {/each}
</div>

<style>
  .poll-list {
    display: grid;
    grid-template-columns: 1fr 1fr;
    grid-gap: 20px;
  }
</style>

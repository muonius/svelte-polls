<script>
  import { onMount } from "svelte";
  import { onDestroy } from "svelte";
  import PollStore from "../stores/PollStore.js";
  import PollDetails from "./PollDetails.svelte";

  export let polls = [];
  //subscribe to PollStore
  const unsub = PollStore.subscribe((data) => {
    polls = data;
  });

  onMount(() => {
    // everytime the component comes back to the DOM, it is mounted
    //get data from db
    console.log("component mounted");
  });

  onDestroy(() => {
    // everytime the component comes back to the DOM, it is mounted
    //get data from db
    console.log("component destoryed");
    unsub();
  });
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

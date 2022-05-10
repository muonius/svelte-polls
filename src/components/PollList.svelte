<script>
  // import { onMount } from "svelte";
  // import { onDestroy } from "svelte";
  // can only use transition elements on html element, not custom element
  import { fade, slide, scale } from "svelte/transition";
  import { flip } from "svelte/animate";
  import PollStore from "../stores/PollStore.js";
  import PollDetails from "./PollDetails.svelte";

  //all the following code block can be omitted
  // export let polls = [];
  //subscribe to PollStore
  // const unsub = PollStore.subscribe((data) => {
  //   polls = data;
  // });

  // onMount(() => {
  //   // everytime the component comes back to the DOM, it is mounted
  //   //get data from db
  //   console.log("component mounted");
  // });

  // onDestroy(() => {
  //   // everytime the component comes back to the DOM, it is mounted
  //   //get data from db
  //   console.log("component destoryed");
  //   unsub();
  // });
</script>

<!-- invoke casting vote event here, event forwarding -->
<div class="poll-list">
  <!-- EASY LIFECYCLE HOOKS, automatically sub and unsub -->
  {#each $PollStore as poll (poll.id)}
    <!-- add subtle transition -->
    <div in:fade out:scale|local animate:flip={{ duration: 500 }}>
      <!-- local means only when one item is removed -->
      <!-- animation adds a slide in event when one card is removed -->
      <!-- <div transition:fade> -->
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
